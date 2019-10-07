<template>
    <div class="article" >
<!--      如果正在加载显示这个loading动画-->
      <div class="loading" v-if="isLoading">
        <img src="../assets/loading.gif" alt="">
      </div>
      <div id="content" v-else>
        <div class="topic_header">
          <div class="topic_title">{{post.title}}</div>
          <ul>
            <li>• 发布于 {{post.create_at | formatDate}}</li>
            <li>• 作者 {{post.author.loginname}}</li>
            <li>• {{post.visit_count}} 次浏览</li>
            <li>• 最后一次编辑是 {{post.last_reply_at | formatDate}}</li>
            <li>• 来自 {{post | tabformatter}}</li>
          </ul>
        </div>
        <div v-html="post.content" class="topic_content"></div>
        <div>
          <div id="reply">
            <div class="topbar">回复</div>
            <div v-for="(reply,index) in post.replies" class="replySec">
              <div class="replyUp">
                <router-link :to="{
                  name:'user_info',
                  params:{
                    name:reply.author.loginname
                }}">
                  <img :src="reply.author.avatar_url" alt="图片加载失败">
                </router-link>
                <router-link :to="{
                name:'user_info',
                params:{
                  name:reply.author.loginname
                }
                }">
                  <span>{{reply.author.loginname}}</span>
                </router-link>
                <span>{{index+1}}楼</span>
                <span>•{{reply.create_at | formatDate}}</span>
                👍&nbsp;&nbsp;
                <span v-if="reply.ups.length > 0">
                {{reply.ups.length}}
                </span>
                <span v-else>0</span>
              </div>
              <p v-html="reply.content" class="replyCon"></p>
            </div>
          </div>
        </div>
      </div>
    </div>

</template>

<script>
    export default {
        name: "Article",
      data(){
          return{
            isLoading:false,  //是否加载动画
            post:{}   //当前文章页的所有内容
          }
      },
      methods:{
          getArticleDate(){
            this.$http.get(`https://cnodejs.org/api/v1/topic/${this.$route.params.id}`)
              .then(res=>{
                if(res.data.success === true){
                  this.isLoading = false
                  this.post = res.data.data
                }
              })
              .catch(function (err) {
                console.log(err)
              })
          }
      },
      beforeMount() {
          this.isLoading = true
          this.getArticleDate()
      },
      watch:{
          '$route'(to,from){
            this.getArticleDate()
          }
      }
    }
</script>

<style>
  @import url('../assets/markdown-github.css');
  .topbar{
    background-color: #f6f6f6;
    font-size: 12px;
    padding: 10px;
    margin-top: 10px;
  }
  .article:not(:first-child){
    margin-right: 340px;
    margin-top: 15px;
  }
  #reply, .topic_header{
    background-color: #fff;
  }
  #reply{
    margin-top: 15px;
  }
  #reply img{
    width: 30px;
    height: 30px;
    position: relative;
    bottom: -9px;
  }
  #reply a,#reply span{
    font-size: 13px;
    color: #666;
    text-decoration: none;
  }
  .replySec{
    border-bottom: 1px solid #e5e5e5;
    padding: 0 10px;
  }
  .loading{
    text-align: center;
    padding-top: 300px;
  }
  .replyUp a:nth-of-type(2){
    margin-left: 0;
    display: inline-block;
  }
  .topic_header{
    padding: 10px;
  }
  .topic_title{
    font-size: 22px;
    font-weight: 700;
    padding-top: 8px;
    font-family: "Helvetica Neue","Luxi Sans","DejaVu Sans",Tahoma,"Hiragino Sans GB",STHeiti,sans-serif!important;
  }
  .topic_header ul{
    margin-bottom: 0!important;
  }
  .topic_header li{
    display: inline-block;
    font-size: 12px;
    color: #838383;
  }
  .topic_content{
    border-top: 1px solid #e5e5e5;
    padding: 10px 20px 10px 20px;
    background: #FFFFFF;
  }
  .markdown-text > h2:nth-child(1){
    margin-top: 15px!important;
  }
  .topic_content ul{
    list-style-type: disc;
    margin: 0 0 10px 25px;
  }
  .topic_content li{
    /*display: block;*/
    color: black;
    font-size: 14px;
    line-height: 2em;
  }
  .markdown-text img{
    width: 92% !important;
  }
  .markdown-text a{
    color: #08c;
    text-decoration: none;
  }
  .markdown-text p{
    white-space: pre-wrap;
  }
  .topic_header h2{
    font-size: 26px;
  }
  .replyCon img{
    height: 100% !important;
  }
  .replyCon p{
    margin-top: 10px!important;
  }
</style>
