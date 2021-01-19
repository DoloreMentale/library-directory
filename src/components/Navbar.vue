<template>
  <v-app-bar app
             dense
             elevate-on-scroll
             color="primary">
    <v-app-bar-title class="white--text">Каталог Библиотек</v-app-bar-title>

    <v-spacer/>

    <v-btn v-if="this.$route.params.id"
           small
           elevation="0"
           class="primary--text"
           @click.prevent="router.push({name: 'Home'})">
      На главную
    </v-btn>

    <v-progress-linear
        :active="loading"
        :indeterminate="loading"
        absolute
        bottom
        color="light-blue accent-1"
    ></v-progress-linear>
  </v-app-bar>
</template>

<script>
import router from "@/router";

export default {
  name: "Navbar",
  data: () => ({
    loading: false,
    router
  }),
  watch: {
    loading(val) {
      if (!val) return

    },
  }
}
</script>

<style scoped>

</style>
