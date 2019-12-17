<template>
  <div id="ml_front">

    <div class="ai_icon">
    <img width="150px" src="@/assets/ai_group_logo.png">
    </div>


    <div class="container">
   
    <div class="input">
      <p>実験条件選択</p>
      <select v-model="selected_condition">
          <option disabled value="">experimental condition</option>
          <option v-for="condition in conditions" v-bind:value="condition.name" v-bind:key="condition.id">
              {{ condition.name }}
          </option>
      </select>
                <p>{{selected_condition}}</p>


      <img width="300px" src="@/assets/train/1_ng/2016-08-08_06-55-44-7290_0.jpg">
      <img width="300px" src="@/assets/train/1_ng/2016-08-10_12-53-59-8100_0.jpg">
      <p>ng samples</p>
      
      <p>学習，評価データ</p>
      <button v-on:click="get_exp_data(exp_data)">get experimental information</button>
      
      <table align="center" style="margin : 20px auto; padding:5px; border :solid 1px #000">
        <tr>
          <th></th>
          <th>ok</th>
          <th>ng</th>
        </tr>
        <tr>
          <td>学習</td>
          <td>{{exp_data.train_ok}}</td>
          <td>{{exp_data.train_ng}}</td>
        </tr>
        <tr>
          <td>評価</td>
          <td>{{exp_data.test_ok}}</td>
          <td>{{exp_data.test_ng}}</td>
        </tr>
      </table>

    </div>

    <div class="select_method">
      <p>select model</p>
      <select v-model="selected_model">
          <option disabled value="">model</option>
          <option v-for="model in models" v-bind:value="String(model.id) + ': '+ String(model.name)" v-bind:key="model.id ">
              {{ model.name }}
          </option>
      </select>
       <p>{{ selected_model}}</p>
      <ul>


        <li>dl or statistic ml</li>
        <li>model</li>
        <li>optimization</li>
        <li>dropout rate</li>
        <li>epoch</li>
        <li>learning rate</li>
        <li>and so on</li>
        <li>start !!!</li>
      </ul>
    </div>

    <div class="result">
      

      <p>result</p>

      <ul>
        <li>reration between epoch and loss</li>
        <li>confusion matrix</li>
        <button v-on:click="get_exp_result(exp_res)">experimental result</button>
        <table>
        <tr>
          <th></th>
          <th>ng</th>
          <th>ok</th>
        </tr>
        <tr>
          <th>ng</th>
          <td>{{exp_res.tp}}</td>
          <td>{{exp_res.fn}}</td>
        </tr>
        <tr>
          <th>ok</th>
          <td>{{exp_res.fp}}</td>
          <td>{{exp_res.tn}}</td>
        </tr>
      </table>


      <table>
        <tr>
          <td>Accuracy</td>
          <td>{{exp_res.acc}} %</td>
        </tr>
        <tr>
          <td>Recall</td>
          <td>{{exp_res.rec}} %</td>
        </tr>
        <tr>
          <td>Precision</td>
          <td>{{exp_res.prec}} %</td>
        </tr>
        <tr>
          <td>Recall</td>
          <td>{{exp_res.rec}} %</td>
        </tr>
      </table>



        <li>acc, recall, prescision, f1-score</li>
        <li>histogram</li>
        <li>roc</li>
      </ul>
    </div>

    <div class="server">
      <p>server information<br>local developing now</p>
      
    
      <ul>
        <li>front : vue (port 172.16.98.152:8080)</li>
        <li>back  : flask (port 172.16.98.152:5000)</li>
        <li>ml    : pytorch, scikit-learn</li>
        <li>db    : mongodb</li>
      </ul>
    </div>

    </div>


    <div class="flow_img">
      <img alt="ml_platform" width="500px" src="./assets/ml_platform.png">
    </div>

  

  </div>
</template>



<script>

// import fs from 'fs';

export default {
  name: 'app',
  data : function() {
    return {
      img_lists : [],
      selected_condition: '',
      conditions: [
          { id: 1, name: 'train:tokushima1, test:tokushima2' },
          { id: 2, name: 'train:tokushima1, test:tokushima1' },
          { id: 3, name: '2 + revised by hinkan' },
          { id: 4, name: '2 + revised by hinkan + kensaki + xc' },
          { id: 5, name: '2 + semisupervised learning' }
      ],
      selected_model: '',
      models: [
          { id: 0, name: 'normal cnn'},
          { id: 1, name: 'vgg16' },
          { id: 2, name: 'resnet18' },
          { id: 3, name: 'mobilenetv3' },
      ],
    counter : 0,
    exp_data : { train_ok : 0, train_ng : 0,test_ok : 0, test_ng : 0}, // important to write like this for Object assign
    exp_res : { tp : 0, fp : 0, fn : 0, tn : 0 ,
                 acc:0, rec:0, prec:0, f1:0}
    }
  },
  methods : {
    get_exp_data (exp_data) {
      // this.axios.get('http://localhost:5000/get_exp_data/').then( res => {
        this.axios.get('http://localhost:5000/get_exp_data/').then( res => {
        Object.assign(exp_data,res.data )
        console.log( exp_data ) 

      });
    },
    get_exp_result (exp_res) {
      this.axios.get('http://localhost:5000/get_exp_result/').then( res => {
        Object.assign(exp_res,res.data )
        console.log( exp_res ) 
      });
    }
  }
}
</script>



<style>

#ml_front {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  
  /* margin-top: 60px; */
}

* {
    box-sizing: border-box;
}

body {
  margin : 0;
  height : 100vh;
  /* background-color : #888888; */
}

.ai_icon{
  margin-top : 10px;
  background-color:white;
}


.flow_img{
  margin-top : 100px;
  background-color:white;
}

.ng_imgs{
  margin : 10px;
}

.container {
  display: block;
  margin-top:30px;
  margin-left: auto;
  margin-right: auto;
  padding : 5px;
  width: 40%;
  /* border : solid 1px #000; */
  background : #eee;
  /* color: #eee; */
  /* width : 50%; */
  text-align :center;
  box-shadow: 0 0 8px gray;
}

.container > * {
  margin : 5% 2% 0 2%;
  /* margin : 5% 1%; */
  padding : 1%;
  box-shadow: 0 0 8px gray;
  background:#fff;
  color : #111;
}
/* 
.input {
  margin : 1%;
  border : solid 1px #000;
  background:#fff;
  color : #111;
}

.select_method{
  margin : 5% 1%;
  padding : 1%;
  box-shadow: 0 0 8px gray;
  background:#fff;
  color : #111;
} */
.container li {
  text-align :left;
}
/* 
.result{
  margin : 1%;
  background:#fff;
  border : solid 1px #000;
  color : #111;
} */

.server {
 margin-bottom : 5%
  /* margin : 1%;
  background:#fff;
  border : solid 1px #000;
  color : #111; */
}

table {
  margin-left:auto; 
  margin-right:auto;
  margin : 30px auto;
  padding:5px; 
  border :solid 1px #000
}


th td {
  padding : 5px;
}




</style>

