<script>

export default {
  name: "ProjectCard",
  props: ["propElement"],
};

</script>

<template>

<div class="col-4">
  <div class="card text-start p-3">
    
    <figure v-if="propElement.cover_image">
      <img class="card-img-top" :src="propElement.cover_image" />
    </figure>

    <div class="card-body">
      <h4 class="card-title">{{ propElement.title }}</h4>

      <ul>
        <li>
          slug: <strong>{{ propElement.slug }}</strong>
        </li>
        <li v-if="propElement.type">
          type: <strong>{{ propElement.type.name }}</strong>
        </li>
        <li>
          technologies:
          <span
            v-for="(technology, index) in propElement.technologies"
            :key="technology.id"
            class="badge rounded-pill text-bg-primary me-1">
            {{ technology.name }}
          </span>
        </li>
      </ul>

      <p class="card-text">{{ propElement.content }}</p>
    </div>
  </div>
</div>

</template>

<style lang="scss" scoped>

@use "../styles/partials/variables" as *;
@use "../styles/partials/mixins" as *;

</style>
