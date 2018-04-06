<template>
  <div class="contain">
    <div class="top-bar">
      <div class="left-icon" @click="goBack()"></div>
      <div class="title">留言板</div>
      <div class="right-icon" @click="editMsg()"></div>
    </div>
    <div class="board-contain">
      <div class="item" v-for="(item, index) in msgList" :key="index">
        <div class="top">
          <div class="img">
            <img :src="item.headPic" width="100%" height="100%">
          </div>
          <div class="username" v-text="item.nickname"></div>
        </div>
        <div class="bottom" v-text="item.text"></div>
      </div>
    </div>
  </div>
</template>
<script type="text/javascript">
  export default {
    data() {
      return {
        msgList: []
      }
    },
    created() {
      // 初始化isBack
      this.$router.isBack = false
      this.initData()
    },
    methods: {
      goBack() {
        this.$router.goBack()
      },
      async initData() {
        // 获取留言数据
       const res = await this.$store.dispatch('getLeaveMsg')
        this.msgList = res.data
      },
      editMsg() {
        this.$router.push({name: 'MsgCreate'})
      }
    }
  }
</script>
<style lang="scss" scoped>
$blue: #12B7F5;
$white: #FFF;
.contain {
  background: #F6F6F6;
  width: 100%;
  height: 100%;
  .top-bar {
    height: 50px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: $blue;
    padding: 0 5px;
    .left-icon {
      width: 30px;
      height: 30px;
      background: url("../assets/img/back.png") no-repeat center / 100%;
    }
    .title {
      font-size: 20px;
      color: $white;
    }
    .right-icon {
      width: 30px;
      height: 30px;
      background: url("../assets/img/edit-icon.png") no-repeat center / 100%;
    }
  }
  .board-contain {
    height: calc(100% - 50px);
    background: #F2F2F2;
    .item {
      background: #FFF;
      margin-top: 5px;
      .top {
        position: relative;
        height: 80px;
        .img {
          position: absolute;
          top: 10px;
          left: 10px;
          width: 55px;
          height: 55px;
          img{
            border-radius: 50%;
          }
        }
        .username {
          position: absolute;
          top:15px;
          left:80px;
          width:30%;
          height:25px;
          overflow: hidden;
          text-overflow:ellipsis;
          white-space: nowrap;
        }
      }
      .bottom {
        padding: 10px 20px 30px 20px;
      }
    }
  }
}
</style>
