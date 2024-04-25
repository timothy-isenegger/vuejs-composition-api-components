<script setup>
import { ref } from 'vue'

const props = defineProps({
  username: {
    type: String,
    required: true
  }
})

const githubProfile = ref()

fetch(`https://api.github.com/users/${props.username}`).then(async (res) => {
  const data = await res.json()
  githubProfile.value = data
})
</script>
<template>
  <div v-if="githubProfile" class="card card-side bg-base-100 shadow-xl m-5">
    <figure>
      <img class="max-h-64" :src="githubProfile.avatar_url" :alt="githubProfile.name" />
    </figure>
    <div class="card-body">
      <h2 class="card-title">{{ githubProfile.name }}</h2>
      <p>
        <strong>Followers: </strong>{{ githubProfile.followers }}<br />
        <strong>Following: </strong>{{ githubProfile.following }}
      </p>
      <div class="card-actions justify-end">
        <a :href="githubProfile.html_url" class="btn btn-primary" target="_blank">View Profile</a>
      </div>
    </div>
  </div>
</template>
