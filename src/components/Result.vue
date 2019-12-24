<template>
  <div class="Result">
      
    <p>RESULT</p>

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


    <ul>
        <li>reration between epoch and loss</li>
        <li>histogram</li>
        <li>roc</li>
    </ul>
  </div>
</template>

<script>

import store from '@/store.js'


export default {
    name: 'Result',
    props: {
        msg: String
    },
    data : function() {
        return {
            exp_data : { train_ok : 0, train_ng : 0,test_ok : 0, test_ng : 0}, // important to write like this for Object assig
            exp_res : { tp : 0, fp : 0, fn : 0, tn : 0,
                        acc:0, rec:0, prec:0, f1:0}
        }
    },
    methods : {
        get_exp_result (exp_res) {
            this.axios.get('http://localhost:5000/get_exp_result/',{
                params : { condition : 1} // 実験条件をrequestで送る．
            }).then( res => {
                console.log(store.state.count)
                Object.assign(exp_res,res.data )
                console.log( exp_res ) 
            });
        }
    }
}

</script>

<style scoped>

.Result {
    margin-bottom : 20px;
}

table {
  margin-left:auto; 
  margin-right:auto;
  margin : 30px auto;
  padding:5px; 
  border :solid 1px #000
}


</style>

