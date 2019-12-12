<template>
  <div id="ml_front">

    <div class="flow_img">
    <img alt="ml_platform" width="250px" src="./assets/ml_platform.png">
    </div>

    <div class="main">
    <div class="input">
      input data
      <ul>
        <li>table</li>
        <li>image</li>
        <li>sound</li>
        <li>time series</li>
      </ul>
    </div>

    <div class="select_method">
      select method
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
      result
      <ul>
        <li>reration between epoch and loss</li>
        <li>confusion matrix</li>
        <li>acc, recall, prescision, f1-score</li>
        <li>histogram</li>
        <li>roc</li>
      </ul>
    </div>

    </div>

  </div>
</template>

<script>

export default {
  name: 'app',
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
  margin-top : 1%;
  background-color:white;
}

.main {
  display: block;
  margin-top:10px;
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


</style>
