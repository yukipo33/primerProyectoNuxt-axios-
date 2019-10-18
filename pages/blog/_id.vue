<template>
  <div>
    <div class="container mt-5">
      <div class="card">
        <div class="card-body">
          <h1>{{ articulo.title }}</h1>
          <p class="small">{{ articulo.nombreAutor }}</p>
          <p>{{ articulo.body }}</p>
          <nuxt-link to="/blog" class="btn btn-dark">Atras</nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import axios from "axios";

export default {
  data() {
    return {
    };
  },
  async asyncData({isDev, route, store, env, params, query, req, res, redirect, error}){
    try {
      const res = await axios.get(`http://jsonplaceholder.typicode.com/posts/${params.id}`)

      let articulo = res.data;

      // console.log('Articulo: ', articulo);

      const resAutor = await axios.get(`https://jsonplaceholder.typicode.com/users/${res.data.userId}`)

      // console.log('Autor: ', resAutor.data);

      articulo.nombreAutor = resAutor.data.name;

      return{
        articulo
      }

    } catch (error) {
      console.log(error);
      return {error: error}
    }
  }

};
</script>
