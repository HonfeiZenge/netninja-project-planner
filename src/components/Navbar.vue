<template>
  <nav class="main__nav">
    <router-link :to="{ name: 'Home' }">Projects</router-link>
    <router-link :to="{ name: 'AddProject' }">Add New Project</router-link>
  </nav>
</template>

<script>
export default {

}
</script>

<style>
  .main__nav {
    text-align: center;
    margin: 40px auto;
  }
  .main__nav a{
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: #999;
    font-size: 18px;
  }
  a.router-link-active {
    border-bottom: 3px solid #00ce89;
    padding-bottom: 4px;
  }
</style>