<template>
  <div class="content">
    <div class="top-bar">
      <div class="left-icon" @click="goBack()"></div>
      <div class="title">留言</div>
      <div class="right-icon">
      </div>
    </div>
    <div class="msg-content">
      <textarea v-model="msgText"></textarea>
      <div class="btn" @click="sendMsg()">
        发送留言
        <div class="icon"><img src="" alt="" width="100%" height="100%"></div>
      </div>
    </div>
  </div>
</template>
<script type="text/javascript">
import {mapGetters} from 'vuex'
import {getItem} from '@/plugin/sessionStorage-plugin.js'
import Alert from '@/components/Alert'
export default {
  data() {
    return {
      msgText: null
    }
  },
  created() {
    this.initData()
  },
  computed: {
    ...mapGetters([
      'getUserinfo'
      ])
  },
  methods: {
    goBack() {
      this.$router.goBack()
    },
    initData() {
      this.$store.commit('setUserinfo', getItem('userInfo'))
    },
    async sendMsg() {
      const MsgData = {
        timeStamp: Date.parse(new Date()),
        userId: this.getUserinfo.userId,
        nickname: this.getUserinfo.nickname,
        headPic: this.getUserinfo.headPic,
        text: this.msgText
      }
      const res = await this.$store.dispatch('saveLeaveMsg', MsgData)
      Alert({content: res.status})
      this.goBack()
    }
  }
}
</script>
<style lang="scss" scoped>
$fontcolor: #FFF;
$m-bg: #12B7F5;
$fontsize: 20px;
$bg: #FFF;
.content {
  background: $bg;
  .top-bar {
    height: 50px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: $m-bg;
    padding: 0 5px;
    .left-icon {
      width: 30px;
      height: 30px;
      background: url("../assets/img/back.png") no-repeat center / 100%;
    }
    .title {
      font-size: $fontsize;
      color: $fontcolor;
    }
    .right-icon {
      width: 30px;
      height: 30px;
    }
  }
  .msg-content {
    display: flex;
    align-items: center;
    flex-direction: column;
    textarea{
      display: block;
      width:80%;
      height: 200px;
      margin-top: 30px;
      border-radius: 5px;
      background: $m-bg;
      color: $fontcolor;
      padding: 15px;
      font-size: $fontsize;
    }
    .btn{
      position: relative;
      width: 50%;
      height: 45px;
      line-height: 45px;
      margin-top: 30px;
      text-align: center;
      border: 1px solid $m-bg;
      border-radius: 6px;
      padding-right: 20px;
      color: $m-bg;
      .icon{
        position: absolute;
        top: 50%;
        right: 10px;
        margin-top: -20px;
        width: 40px;
        height: 40px;
        background: red;
        background: url("../assets/img/paper.png") no-repeat center / 100%;
      }
    }
  }
}
</style>
