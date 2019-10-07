<template>
  <div class="UserInfo">
    <!--      如果正在加载显示这个loading动画-->
    <div class="loading" v-if="isLoading">
      <img src="../assets/loading.gif" alt="">
    </div>
    <div class="userInfomation" v-else>
      <section>
        <img :src="userInfo.avatar_url" alt="图片下载错误">
        <span>{{userInfo.loginname}}</span><br>
        <p>{{userInfo.score}} 积分</p>
        <p>注册时间 {{userInfo.create_at | formatDate}}</p>
      </section>
      <div class="replies">
        <p>回复的主题</p>
          <ul>
            <li v-for="item in userInfo.recent_replies">
              <router-link :to="{
                name:'post_content',
                params:{
                  id:item.id
                }
              }">
                {{item.title}}
              </router-link>
            </li>
          </ul>
      </div>
      <div class="topics">
        <p>创建的主题</p>
        <ul>
          <li v-for="item in userInfo.recent_topics">
            <router-link :to="{
                name:'post_content',
                params:{
                  id:item.id
                }
              }">
              {{item.title}}
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
    export default {
        name: "UserInfo",
        data(){
          return{
            isLoading:false,
            userInfo:{}
          }
        },
        methods:{
          getUserInfoData(){
            this.$http.get(`https://cnodejs.org/api/v1/user/${this.$route.params.name}`)
              .then(res=>{
                if(res.data.success === true){
                  console.log(res)
                  this.isLoading = false
                  this.userInfo = res.data.data
                }
              })
              .catch(function (err) {
                console.log(err)
              })
          }
        },
        beforeMount() {
            this.isLoading = true
            this.getUserInfoData()
        }
    }
</script>

<style scoped>
  .userInfomation{
    background: white;
    width: 100%;
    margin: 10px auto;
  }
  .userInfomation section{
    padding: 12px;
  }
  .userInfomation img{
    width: 30px;
  }
  .userInfomation li{
    list-style: none;
  }
  .userInfomation .replies,
  .userInfomation .topics{
    font-size: 0.72rem;
    border-top: 10px #dddddd solid;
  }
  .userInfomation > div > p{
    padding: 12px 0 12px 12px;
    background-color: rgba(212,205,205,0.17);
    font-size: 0.75rem;
    margin: 0;
  }
  .userInfomation > div > ul{
    padding-left: 0;
  }
  .userInfomation > div > ul > li{
    padding: 4px 0 4px 12px;
    white-space: nowrap;
    font-size: 16px;
    text-overflow: ellipsis;
    overflow: hidden;
    line-height: 30px;
    vertical-align: middle;
  }
  .userInfomation > div > ul > li > a{
    color: #094e99;
    text-decoration: none;
  }
</style>
