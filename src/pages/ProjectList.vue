<script>

import axios from 'axios';
import ProjectCard from './ProjectCard.vue';

export default {
  components:{
    ProjectCard
  },
  name: "ProjectList",
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

  <main class="container">

    <h2 class="m-5">Projects</h2>

    <div class="container mb-5">
        <div class="row">
            <li v-for="( element, index) in arrayProjects" :key="element.id">
                <router-link :to="{ name: 'single-project', params: {slug: element.slug} }">
                    {{  element.title }}
                </router-link>
            </li>
        </div>
    </div>

    <nav aria-label="Page navigation example">
        <ul class="pagination">
        <li class="page-item" :class="{ 'disabled': currentPage === 1 }">
            <button class="page-link" @click="getProjects( currentPage - 1 )">Previous</button>
        </li>

        <li class="page-item" v-for=" (element,index) in lastPage" :key="index">
            <button class="page-link"  @click="getProjects( element )">{{ element }}</button>
        </li>
        
        <li class="page-item" :class="{ 'disabled': currentPage === lastPage }">
            <button class="page-link" @click="getProjects( currentPage + 1 )">Next</button>
        </li>
        </ul>
    </nav>

  </main>
  
</template>

<style lang="scss" scoped>
@use "../styles/partials/variables" as *;
@use "../styles/partials/mixins" as *;

</style>
