<template>
    <div class="header">
      <div class="header-inner">
        <div class="container">
          <router-link :to="{name:'root'}">
            <img src="../assets/cnodejs_light.svg" alt="图片显示失败 ">
          </router-link>
          <ul>
            <li><a href="#">首页</a></li>
            <li><a href="#">新手入门</a></li>
            <li><a href="#">API</a></li>
            <li><a href="#">关于</a></li>
            <li><a href="#">注册</a></li>
            <li><a href="#">登录</a></li>
          </ul>
        </div>
      </div>
    </div>
</template>

<script>
    export default {
        name: "Header"
    }
</script>

<style scoped>
.header{
  background-color: #444444;
  height: 50px;
}
.header-inner{
  width: 90%;
  margin: auto;
  padding: 5px;
}
.container{
  width: 100%;
  min-width: 960px;
  max-width: 1400px;
  margin: 0 auto;
}
img{
  max-width: 120px;
  margin-top: 3px;
}
ul{
  list-style: none;
  float: right;
  display: inline-block;
  margin: 0;
  padding: 0;
}
li{
  display: inline-block;
  padding: 10px 15px;
  float: left;
}
a{
  text-decoration: none;
  color: #ccc;
  font-size: 13px;
  text-shadow: none;
  font-family: "Helvetica Neue","Luxi Sans","DejaVu Sans",Tahoma,"Hiragino Sans GB",STHeiti,sans-serif!important;
}
</style>
