<template>
  <div id="ml_front">

  

    <div class="main">
    <div class="input">
      <p>実験条件選択</p>
      <select v-model="selected_condition">
          <option disabled value="">experimental condition</option>
          <option v-for="condition in conditions" v-bind:value="condition.name" v-bind:key="condition.id">
              {{ condition.name }}
          </option>
      </select>
                <p>{{selected_condition}}</p>

      
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
        <li>acc, recall, prescision, f1-score</li>
        <li>histogram</li>
        <li>roc</li>
      </ul>
    </div>

    <div class="result">
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


export default {
  name: 'app',
  data : function() {
    return {
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

.flow_img{
  margin-top : 100px;
  background-color:white;
}

.main {
  display: block;
  margin-top:5%;
  margin-left: auto;
  margin-right: auto;
  padding : 5px;
  width: 40%;
  border : solid 1px #000;
  color: #111;
  /* width : 50%; */
  text-align :center;
}

.input {
  margin : 1%;
  border : solid 1px #000;
  color : #111;
}

.select_method{
  margin : 1%;
  border : solid 1px #000;
  color : #111;
}
.main li {
  text-align :left;
}

.result{
  margin : 1%;
  border : solid 1px #000;
  color : #111;
}

.server {
   margin : 1%;
  border : solid 1px #000;
  color : #111;
}

th td {
  padding : 5px;
}




</style>

