<template>
<div class="container">
   <h1 v-if="is_admin == 'true' ">HI Admin,</h1>
      <h1 v-else>HI {{first_name}},</h1>
  <div class="row">
    <div class="col-lg-6" v-if="is_admin == 'true' ">
      <input
        type="text"
        v-model="title"
        class="from-control mt-2"
        placeholder="Title"
      /> <br>
      <input
        type="text"
        v-model="catagory"
        class="from-control mt-2"
        placeholder="Category"
      /> <br>
      <input
        type="text"
        v-model="published_date"
        class="from-control mt-2"
        placeholder="publisheddate YYYY-MM-DD"
      /> <br>

      <button @click="add" class="btn btn-block btn-success mt-2">ADD/SAVE</button>
    </div>
    <div class="col-lg-6">
      <table class="table">
        <thead>
          <th>TITLE</th>
          <th>CATEGORY</th>
          <th>PUBLISH DATE</th>
          <th v-if="is_admin == 'true'">EDIT</th>
          <th v-if="is_admin == 'true'"> DELETE</th>
        </thead>
        <tbody>
          <tr v-for="book in books" v-bind:key="book.id">
            <td>{{ book.title }}</td>
            <td>{{ book.catagory }}</td>
            <td>{{ book.published_date }}</td>
            <td v-if="is_admin == 'true'">
              <button @click="getOne(book)" class="btn bn-sm btn-success">
                <i class="bi-pencil"></i>
              </button>
            </td>
            <td v-if="is_admin == 'true'">
              <button @click="deleteOne(book.id)" class="btn bn-sm btn-danger">
                <i class="bi-trash-fill"></i>
              </button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'Container',
  props: {
    msg: String
  },
  data(){
    return{
      id: '',
      title: '',
      catagory: '',
      published_date: '',
      books: null,
      is_admin : localStorage.getItem("is_admin"),
      first_name: localStorage.getItem("first_name")
    }
  },
  mounted(){
    this.getAll();
  },
  methods:{
    getAll(){
      axios.get(`http://localhost:8000/api/book`)
      .then((res)=>{
        this.books=res.data
        this.id = ''
        this.title = '',
        this.catagory = '',
        this.published_date = ''
        })
    },
    getOne(book){
      this.title = book.title,
      this.catagory = book.catagory,
      this.published_date = book.published_date
      this.id = book.id

    },
    deleteOne(id){
      axios.delete(`http://localhost:8000/api/book/${id}/`)
      .then(()=>{
        this.getAll()
      })
    },
    add(){
      console.log(this.title);
      if (this.id =='') {

      axios.post(`http://127.0.0.1:8000/api/book/`,
      {title:this.title,catagory:this.catagory,published_date:this.published_date
      })
      .then(()=>{
        this.getAll()
      })
    
        
      } else {
      axios.put(`http://localhost:8000/api/book/${this.id}/`,
      {title:this.title,catagory:this.catagory,published_date:this.published_date
      })
      .then(()=>{
        this.getAll()
      })
    
      }
     
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
