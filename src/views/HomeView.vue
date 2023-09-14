<template>
  <div class="home container mx-auto px-8 py-8">
    <div class="columns-3 gap-8">
      <router-link v-for="app in apps" :key="app.link" :to="`/${app.link}`">
        <div
          class="card card-side bg-base-200 hover:bg-base-300 shadow-sm mb-8"
        >
          <figure>
            <img :src="app.imageURL" alt="Movie" />
          </figure>
          <div class="card-body">
            <h2 class="card-title">{{ app.label }}</h2>
            <p>{{ app.description }}</p>
          </div>
        </div>
      </router-link>
    </div>
  </div>
</template>

<script setup lang="ts">
const apps = [
  {
    link: 'gradients',
    label: 'Gradients',
    description: 'A collection of gradients that can be used in applications.',
    imageURL: 'https://picsum.photos/160/210'
  },
  {
    link: 'waves',
    label: 'Waves',
    description: 'A collection of gradients that can be used in applications.',
    imageURL: 'https://picsum.photos/160/210'
  },
  {
    link: 'icons',
    label: 'Icons',
    description: 'A collection of gradients that can be used in applications.',
    imageURL: 'https://picsum.photos/160/210'
  }
]
</script>
