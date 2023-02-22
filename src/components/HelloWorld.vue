<template>
  <div id="app">
    <div id="calWrap">
      <div class="top">
        <input type="text" v-model="result" />
      </div>
      <div id="keys">
        <input type="button" value="MC" @click="mcOperation" />
        <input type="button" value="MR" @click="mrOperation" />
        <input type="button" value="MS" @click="msOperation" />
        <input type="button" value="M+" @click="mAddOperation" />
        <input type="button" value="9" @click="key" />
        <input type="button" value="8" @click="key" />
        <input type="button" value="7" @click="key" />
        <input type="button" value="*" @click="key" />
        <input type="button" value="6" @click="key" />
        <input type="button" value="5" @click="key" />
        <input type="button" value="4" @click="key" />
        <input type="button" value="/" @click="key" />
        <input type="button" value="3" @click="key" />
        <input type="button" value="2" @click="key" />
        <input type="button" value="1" @click="key" />
        <input type="button" value="+" @click="key" />
        <input type="button" value="." @click="key" />
        <input type="button" value="0" @click="key" class="zero" />
        <input type="button" value="-" @click="key" />
        <input type="button" value="=" @click="calculate" />
        <input type="button" value="C" @click="clear" class="clear" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  data: () => ({
    result: "",
  }),
  methods: {
    key(event){
      console.log(event.target.value);
      this.result = this.result + event.target.value;
      

          },
    clear() {
      this.result = "";
    },
    async calculate(){
      let newValue ={
        client : this.result
      }
      const response = await axios.post("http://127.0.0.1:8000/calculation/",newValue);
      console.log(response.data);
      this.result = response.data;
    },
    async mcOperation(){
      const response = await axios.get("http://127.0.0.1:8000/mcoperation/");
      console.log(response.data);
      this.result = "";
    },
    async msOperation() {
      let newValue ={
        client : this.result
      } 
      const response = await axios.post("http://127.0.0.1:8000/msoperation/", 
        newValue,
      );
      console.log(response.data);
      this.result = response.data;
    },
    async mrOperation(){
      let newValue ={
        client : this.result
      } 
      const response = await axios.get(
        "http://127.0.0.1:8000/mroperation/",newValue
      );
      console.log(response.data);
      this.result = response.data;
    },
    async mAddOperation(){
      let newValue ={
        client : this.result
      } ;
      const response = await axios.put(
        "http://127.0.0.1:8000/maddoperation/",newValue 
      );
      console.log(response.data);
      this.result = response.data;
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url(https://fonts.googleapis.com/css?family=Open+Sans:400,700);
/***********************************************************************************************/
/* =Common Styles */
/***********************************************************************************************/
body {
  font-family: "Open Sans", sans-serif;
  background-color: #4894d6;
}
body #calWrap {
  background-color: #77889a;
  border-radius: 23px;
  padding: 2em 1em 1em 1em;
  margin: auto;
  width: 292px;
  clear: both;
  display: table;
}
body .top input {
  height: 36px;
  width: 90%;
  font-size: 13px;
  font-weight: bold;
  border-radius: 4px;
  margin: 0 0 14px 0;
  border: 0;
  padding: 0 1em;
  box-shadow: 0px 4px rgba(0, 0, 0, 0.2);
}
body #keys input {
  cursor: pointer;
  width: 66px;
  height: 36px;
  font-weight: bold;
  text-align: center;
  line-height: 2em;
  background: white;
  border-radius: 3px;
  box-shadow: 0px 4px rgba(0, 0, 0, 0.2);
  margin: 0 7px 11px 0;
  float: left;
  transition: all 0.2s ease;
}
body #keys input:hover {
  background-color: #d6d6d6;
}
body #keys .zero {
  width: 138px !important;
}
body #keys .clear {
  background-color: #ffd900 !important;
}
</style>
