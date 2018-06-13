<template>

  <div>
    <h3>A custom Component</h3>
    <p :products="theProducts" the-title="Shop our award- winning product lines"></p>
    <h2>{{theTitle}}</h2>
    <div class="product-list">
    <ul>
      <li v-for="product in products">
        <img :src="product.image">
        <p>{{product.description}}</p>
      </li>
    </ul>
  </div>
  </div>
</template>

<script>
  /*
  * @todo resolve these issue of rendering the page. */
  import  axios from 'axios';
  export default {
    data() {
      return {
      theProducts:[]
      }
    },
    created: function(){
      axios.get('https://hplussport.com/api/products')
        .then((res) =>{
          this.theProducts = res.data
        })
    }
  }

</script>

<style scoped>
  .product-list h2 {
    margin-bottom: 40px;
  }
  .product-list ul img {
    float: left;
    width: 300px;
  }
  .product-list ul {
    list-style-type: none;
  }
  .product-list li {
    margin-bottom: 40px;
    clear: both;
  }

</style>
