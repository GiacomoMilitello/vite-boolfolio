<script>
import axios from 'axios';

export default {
  name: "ProjectCard",
  data() {
    return {
      project: null,
    };
  },
  async mounted() {
    const slug = this.$route.params.slug;
    const response = await axios.get(`http://127.0.0.1:8000/api/test/${slug}`);
    this.project = response.data.project;
  },
};
</script>

<template>

<div class="col-4">
  <div class="card text-start p-3">
    
    <figure v-if="project && project.cover_image">
      <img class="card-img-top" :src="project.cover_image" />
    </figure>

    <div class="card-body">
      <h4 class="card-title">{{ project && project.title }}</h4>

      <ul>
        <li>
          slug: <strong>{{ project && project.slug }}</strong>
        </li>
        <li v-if="project && project.type">
          type: <strong>{{ project.type.name }}</strong>
        </li>
        <li v-if="project && project.technologies">
          technologies:
          <span
            v-for="(technology, index) in project.technologies"
            :key="technology.id"
            class="badge rounded-pill text-bg-primary me-1">
            {{ technology.name }}
          </span>
        </li>
      </ul>

      <p class="card-text">{{ project && project.content }}</p>
    </div>
  </div>
</div>

</template>

<style lang="scss" scoped>

@use "../styles/partials/variables" as *;
@use "../styles/partials/mixins" as *;

</style>
