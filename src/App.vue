<template>
  <div id="app">
    <UserSearch />
  </div>
</template>

<script>
import UserSearch from './components/UserSearch.vue'

export default {
  name: 'App',
  components: {
    UserSearch
  }
}
</script>

<style>
@import "https://cdn.jsdelivr.net/npm/bulma@0.9.2/css/bulma.min.css"
</style>
