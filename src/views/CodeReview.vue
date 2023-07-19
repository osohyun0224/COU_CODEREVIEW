<template>
  <div class="flex-container">
    <div class="header">
      <div class="cdreview_title" slot="title">{{ mainTitle }}</div>
      <button type="button" id="add-new" @click="Create">+</button>
    </div>
    <Card :padding="20" class="reviewContainer">
      <div class="reviewBox markdown-body">
        <ul v-if="mainItem && mainItem.length" @click="gotoDetail">
          <li v-for="(item, index) in mainItem" :key="index">
            <p>{{ item.title }}</p>
            <p>Username: {{ item.username }}</p>
            <p>Create Time: {{ item.create_time }}</p>
            <p>Comment Count: {{ item.comment_count }}</p>
            <!--<p>Code: {{ item.code }}</p>-->
          </li>
        </ul>
        <p v-else>Loading...</p>
      </div>
    </Card>
    <div style="display:flex; justify-content: center">
      <div style="float:right">
        <Pagination :total="total" :page-size="limit" @on-change="changeRoute" :current.sync="page"></Pagination>
      </div>
    </div>
  </div>
</template>

<script>
  import api from '@oj/api'
  import Pagination from '@/pages/oj/components/Pagination'
  
  export default {
    components: {
      Pagination
    },
    data () {
      return {
        mainTitle: '코드리뷰',
        mainItem: [] // 빈 배열로 초기화
      }
    },
    mounted () {
      this.codeReviewMain()
    },
    methods: {
      Create () {
        this.$router.push({name: 'createcodereview'}).catch(() => {})
      },
      codeReviewMain () {
        api.codeReviewMain().then(res => {
          this.mainItem = res.data
          console.log(this.mainItem)
        }).catch(() => {
          this.loadingTable = false
        })
      },
      gotoDetail () {
        this.$router.push({name: 'codereviewdetail'}).catch(() => {})
      }
    }
  }
</script>

<style scoped lang="less">
  .flex-container {
    width : 100%;
    height : 100%;
    padding : 0 50px 0 50px;
    margin : 0;
    display : flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .header {
    width : 100%;
    height : 100%;
    display : flex;
    justify-content: space-between;
    align-items: center;
  }

  .cdreview_title {
    padding-top : 50px;
    margin-left : 50px;
    font-size : 1.75rem;
    font-weight : 700;
  }

  #add-new {
    width : 35px;
    height : 35px;
    font-size: 30px;
    font-weight: 400;
    line-height: 35px;
    margin-right: 50px;
    margin-top: 50px;
    color : gray;
    background-color: white;
    border: 1px solid gray;
    transition: all 0.3s ease-in-out;
    cursor: pointer;
  }

  #add-new:hover {
    background-color: orange;
    color: rgb(171, 112, 0);
    border: 1px solid rgb(171, 112, 0);
  }

  .reviewContainer {
    width : 95%;
    margin : 50px 0 0 0;
    cursor: pointer;
  }

  .reviewBox {
    width : 100%;
    padding : 20px;
    margin : 0;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .reviewBox ul {
    width : 100%;
    height : 150px;
  }

  .reviewBox ul li {
    margin-top : 20px;
    height : 150px;
  }

  .reviewBox ul li p{
    color : black;
  }
</style>