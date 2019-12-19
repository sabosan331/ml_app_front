<template>
  <div id="ml_front">

    <div class="container">
      <h1 class="title">ML App.</h1>
      <Condition />
      <ModelSelect />
      <Result />
    </div>

  </div>
</template>



<script>

// import fs from 'fs';
import Condition from "./components/Condition";
import ModelSelect from "./components/ModelSelect";
import Result from "./components/Result";
// import { count } from './store/store';


export default {
  name: 'app',
  components :{
    Condition,
    ModelSelect,
    Result
  },
  data : function() {
    return {
    }
  },
}
</script>

<style>
* {
    box-sizing: border-box;
}
body {
  margin : 0;
  height : 100vh;
  background : #fff;
}
.title {
  background-color : #eaeaea !important;
  /* border-bottom : solid 2px #000000; */
  box-shadow: none !important;
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
  background : #eaeaea;
  text-align :center;
  box-shadow: 0 0 8px gray;
}
.container > * {
  margin : 5% 2% 0 2%;
  padding : 1%;
  box-shadow: 0 0 8px gray;
  background:#fff;
  color : #111;
}
.container li {
  text-align :left;
}
th td {
  padding : 5px;
}
</style>
