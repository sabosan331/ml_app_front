<template>
  <div class="ModelSlect">

    <div class="select_method">
      <h4>MODEL SELECT</h4>
      <select v-model="selected_model">
          <option disabled value="">model</option>
          <option v-for="model in models" v-bind:value="String(model.id) + ': '+ String(model.name)" v-bind:key="model.id ">
              {{ model.name }}
          </option>
      </select>
       <p>{{ selected_model}}</p>
      <!-- <ul>


        <li>dl or statistic ml</li>
        <li>model</li>
        <li>optimization</li>
        <li>dropout rate</li>
        <li>epoch</li>
        <li>learning rate</li>
        <li>and so on</li>
        <li>start !!!</li>
      </ul> -->
       <button v-on:click="get_exp_result">training start !!!</button>

    </div>  
    
  </div>
</template>

<script>
export default {
    name: 'ModelSelect',
    props: {
        msg: String
    },
    data : function() {
        return {
            selected_model: '',
            models: [
                { id: 0, name: 'normal cnn'},
                { id: 1, name: 'vgg16' },
                { id: 2, name: 'resnet18' },
                { id: 3, name: 'mobilenetv3' },
            ],
        }
    },
    methods : {
        get_exp_result (exp_res) {
            this.axios.get('http://localhost:5000/get_exp_result/').then( res => {
                Object.assign(exp_res,res.data )
                console.log( exp_res ) 
            });
        }
    }
}

</script>

<style scoped>

table {
  margin-left:auto; 
  margin-right:auto;
  margin : 30px auto;
  padding:5px; 
  border :solid 1px #000
}


</style>

