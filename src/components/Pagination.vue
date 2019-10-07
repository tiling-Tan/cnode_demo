<template>
  <div class="pagination">
    <button @click="changebtn">首页</button>
    <button @click="changebtn">上一页</button>
    <button v-if="jduge" class="pagebtn">…</button>
    <button v-for="btn in pagebtns"
            @click="changebtn(btn)"
    :class="[{currentPage: btn === currentPage},'pagebtn']">
      {{btn}}
    </button>
    <button @click="changebtn">下一页</button>
  </div>
</template>

<script>
  import $ from 'jquery'
    export default {
        name: "Pagination",
        data(){
          return{
            pagebtns:[1,2,3,4,5,"…"],
            currentPage:1,
            jduge:false
          }
        },
      methods:{
        changebtn(page){
          if(typeof page != 'number'){
            //点击的是上一页、下一页或者首页
            switch (page.target.innerHTML) {
              case '上一页':
                $('button.currentPage').prev().click()
                    break
              case '下一页':
                $('button.currentPage').next().click()
                    break
              case '首页':
                this.pagebtns = [1,2,3,4,5,"…"]
                this.changebtn(1)
                    break
              default:break
            }
            return
          }
          this.currentPage = page
          if(page > 4){
            this.jduge = true
          }else{
            this.jduge = false
          }
          if(page === this.pagebtns[4]){
            this.pagebtns.shift()
            this.pagebtns.splice(4,0,this.pagebtns[3]+1)
          }else if(page === this.pagebtns[0] && page>1){
            this.pagebtns.splice(4,1)
            this.pagebtns.unshift(this.pagebtns[0]-1)

          }
          this.$emit('handleList',this.currentPage)
        }
      }
    }
</script>

<style scoped>
  .pagination{
    margin-top: 5px;
    margin-bottom: 20px;
    background-color: white;
    padding: 6px 20px;
    border-radius: 5px;
    border: 1px solid #888888;
  }
  button{
    background-color: #ffffff;
    border: 1px solid #dddddd;
    color: #778087;
    border-radius: 3px;
    outline: none;
    height: 21px;
    cursor: pointer;
    padding: 0 2px;
    width: 55px;
    height: 29px;
  }
  .pagebtn{
    position: relative;
    bottom: 1px;
    width: 40px;
    margin: 0 4px;
  }
  .currentPage{
    color: white;
    background-color: #1f1b1b;
  }
</style>
