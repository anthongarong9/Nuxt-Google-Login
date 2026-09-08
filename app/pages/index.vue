<template>
  <v-container v-if="user" class="pa-6">
    <div class="d-flex align-center ga-4 mb-4">
      <v-avatar size="64"><v-img :src="user.picture" /></v-avatar>
      <div>
        <h2>{{ user.name }}</h2>
        <p>{{ user.email }}</p>
      </div>
    </div>
    <v-btn color="error" @click="logout">Logout</v-btn>
  </v-container>
</template>

<script setup lang="ts">
const user = ref<any>(null)

onMounted(() => {
  const saved = localStorage.getItem('google_user')
  if (saved) {
    user.value = JSON.parse(saved)
  } else {
    // Kapag walang saved user, rekta agad sa /login page
    navigateTo('/login')
  }
})

const logout = () => {
  localStorage.removeItem('google_user')
  localStorage.removeItem('google_token')
  navigateTo('/login')
}
</script>