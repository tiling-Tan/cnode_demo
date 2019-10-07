<template>
  <div id="app">
    <Header/>
    <div class="main">
      <router-view name="slidebar"></router-view>
      <router-view name="main"></router-view>
    </div>
  </div>
</template>

<script>
  import Header from './components/Header'
  import postList from './components/postList'
export default {
  name: 'App',
  components:{
    Header,
    postList
  }
}
</script>

<style scoped>
.main{
  width: 73.5%;
  margin:0 auto;
}
  #app{
    background-color: #E1E1E1;
    min-height: 100vh;
  }
</style>
