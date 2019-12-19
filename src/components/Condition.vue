<template>
  <div class="Condition">
      <p>Experimental Condition</p>
      <select v-model="selected_condition">
          <option disabled value="">experimental condition</option>
          <option v-for="condition in conditions" v-bind:value="condition.name" v-bind:key="condition.id">
              {{ condition.name }}
          </option>
      </select>
                <p>{{selected_condition}}</p>


      <img width="150px" src="@/assets/train/1_ng/2016-08-08_06-55-44-7290_0.jpg" style="padding : 5px">
      <img width="150px" src="@/assets/train/1_ng/2016-08-10_12-53-59-8100_0.jpg" style="padding : 5px">
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
</template>

<script>
export default {
    name: 'Condition',
    props: {
        msg: String
    },
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
            exp_data : { train_ok : 0, train_ng : 0,test_ok : 0, test_ng : 0},
        }
    },
    methods : {
        get_exp_data (exp_data) {
            this.axios.get('http://localhost:5000/get_exp_data/').then( res => {
                Object.assign(exp_data,res.data )
                console.log( exp_data ) 
            });
        },
    }
}

</script>

<style scoped>

table {
    margin-left:auto; 
    margin-right:auto;
    margin : 30px auto;
    padding:10px; 
    border :solid 1px #000;
}

td th {
    border :solid 1px #000;
    padding:10px; 
}


</style>
