<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <a :href="url">Home</a>
    <form>
      Name: <label>
      <input type="text" :value="name"/>
    </label>
    </form>
    <hr/>
    <h3>Computed</h3>
    <div>
      <label>
       Fahrenheit: <input type="text" v-model.number.lazy="tempFahrenheit"/>
      </label>
      Temperature in Celsius: {{tempCelsius}}
    </div>
    <hr/>
    <h3>Watchers</h3>
    <div>
      <h3>Got a question for our virtual agent?</h3>
      <label>
        Just ask!: <input type="text" v-model="question"/>
      </label>
      {{response}}
      <ul>
        <li v-for="product in products">{{product.name}}</li>
      </ul>
    </div>
    <hr/>
    <local-component></local-component>
    <local-component></local-component>
    <hr/>
    <global-component></global-component>
    <hr/>
    <h3>Custom Component</h3>
    <custom-component></custom-component>
  </div>
</template>
<script>
  import customComponent from './customComponent';
  import axios from 'axios';
  import Vue from "../router";

  // Vue.component('global-component', {
  //   template: '<div> a global component</div>'
  // });
// SHOWS HOW LOCAL COMPONENTS CAN BE INDEPENDENT
  const localComponent = { template: '<div @click="showNum()">\
    A local component\
    <div>The number: {{num}}</div>\
  </div>',
  data: function () {
    return{
      num: Math.random()
    };
  },
    methods: {
    showNum: function(){
      alert('My number is ' + this.num);
    }
    }
  };
export default {
  data () {
    return {
      msg: 'Hello Aima',
      url: 'https://www.google.com',
      name: 'Aimable',
      tempFahrenheit: 0,
      question: '',
      response: '',
      products: []
    }
  },
  props: ['theTitle', 'products'],
  components: {
    'local-component': localComponent,
    'custom-component': customComponent
  },
  beforeCreate: function () {
    console.log('beforeCreate')
  },
  created: function(){
    console.log('created');
    this.question = 'A default question about products';
  },
  beforeMount: function(){
    console.log("beforeMount")
  },
  mounted: function(){
    console.log("mounted")
  },
  beforeUpdate: function(){
    console.log("beforeUpdate")
  },
  updated: function(){
    console.log("updated")
  },
  beforeDestroy: function(){
    console.log('beforeDestroy')
  },
  destroyed: function(){
    console.log('destroyed')
  },
  computed:{
    tempCelsius: function(){
      return Math.round(5/9 * (this.tempFahrenheit -32))
    },
    products: function(){
      // this needs to return a value immediately, can't wait for ajax response
    }
  },
  watch: {
    question: function(newValue){
      if(newValue.indexOf('products') > -1){
        console.log('API Call');
        this.response = 'Sure I can list the products for you: ';
        axios.get('https://hplussport.com/api/products')
          .then((res) => {
            console.log('API response');
            this.products = res.data;
          })
          .catch((err) =>{
            console.log(err)
        })
      }
      else {
        this.response = "Sorry, I don't understand that question."
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
