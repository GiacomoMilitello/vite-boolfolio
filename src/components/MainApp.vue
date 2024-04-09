<script>

import axios from 'axios';

export default {
  name: "MainApp",
  data(){
    return{
      arrayProjects: [],
      currentPage:'',
      lastPage:'',
    }
  },
  methods: {
    getProjects( projectApiPage){

      axios.get( 'http://127.0.0.1:8000/api/test',
        {
          params: {
            page: projectApiPage
          }
        }
      )
        .then( res => {
          console.log( res.data.projects.data )

          this.arrayProjects = res.data.projects.data
          this.currentPage = res.data.projects.current_page
          this.lastPage = res.data.projects.last_page
        })

    }
  },
  mounted(){
    this.getProjects( 1 )
  }
};


</script>

<template>

  <h2>Projects</h2>

  <ul>
    <li v-for="(element,index) in arrayProjects" :key="element.id">
      <a href="#">{{ element.title }}</a>
    </li>
  </ul>

  <nav aria-label="Page navigation example">
    <ul class="pagination">
      <li class="page-item" :class="{ 'disabled': currentPage === 1 }">
        <button class="page-link" @click="getProjects( currentPage - 1 )">Previous</button>
      </li>
      
      <li class="page-item" :class="{ 'disabled': currentPage === lastPage }">
        <button class="page-link" @click="getProjects( currentPage + 1 )">Next</button>
      </li>
    </ul>
</nav>
  
</template>

<style lang="scss" scoped>
@use "../styles/partials/variables" as *;
@use "../styles/partials/mixins" as *;

</style>
