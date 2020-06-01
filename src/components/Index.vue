<template>
  <div class="index container">
    <div class="card" v-for="cat in moviesLibrary" :key="cat.id">
      <i class="material-icons delete" @click="deleteCategory(cat.id)">delete</i>
      <div class="card-content">
        <h2 class="indigo-text">{{ cat.category }}</h2>
        <ul class="movies">
          <li v-for="(movie, index) in cat.movies" :key="index">
            <span class="chip">{{ movie }}</span>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import db from '@/firebase/init'


export default {
  name: 'Index',
  data () {
    return {
     moviesLibrary: []
    }
  },
  methods: {
    deleteCategory(id){
      
      this.moviesLibrary = this.moviesLibrary.filter(cat => {
      return cat.id != id
        
      })
    },
    created(){
      // fetch data from firestore
      db.collection("moviesLibrary").get()
        .then( snapshot => {
          snapshot.forEach(doc => {
            console.log(doc.data())
            // let cat = doc.data()
            // cat.id = doc.id
            // this.moviesLibrary.push(cat)
          })
        })
    }
  }
}
</script>

<style >
.index{
  display: grid;
  grid-template-columns:1fr 1fr 1fr; ; 
  grid-gap: 30px;
  margin-top: 60px;
}
.index h2{
  font-size: 1.8em;
  text-align: center;
  margin-top: 0;
}
.index .movies{
  margin: 10px auto;
  display: table;
}
.index .movies li{
  display: inline-block;
}
.index .delete{
  position: absolute;
  top: 4px;
  right: 4px;
  cursor: pointer;
  color: #aaa;
  font: 1.4em;
}
</style>
