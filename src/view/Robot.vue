<template>
  <div class="content">
    <div class="msg-content">
      <div v-for="(msg,index) in MsgList" :key="index">
        <other-msg :msg="msg" :index="index" v-if="msg.userId!=getUserinfo.userId"></other-msg>
        <my-msg :msg="msg" v-else></my-msg>
      </div>
    </div>
    <div class="bottom-bar">
      <input type="text" v-model="inputText"/>
      <div class="btn-default" v-if="inputText==''">发送</div>
      <div class="btn-active" v-else  @click="submit">发送</div>
    </div>
  </div>
</template>
<script type="text/javascript">
import io from 'socket.io-client'
import {mapGetters} from 'vuex'
import MyMsg from '@/components/Msg/MyMsg'
import OtherMsg from '@/components/Msg/OtherMsg'
  export default {
    data() {
      return {
        socket: null,
        inputText: '',
        MsgList: [],
        msgDOM: null
      }
    },
    created() {
      this.InitRobot()
    },
    mounted() {
      this.msgDOM = document.querySelector('.msg-content')
      // this.socket = io('http://localhost:3000')
      this.socket = io('http://www.chenleiming.com:3000')
      this.socket.on('robot-msg', (robotMsg) => {
        this.MsgList.push(robotMsg)
        this.$nextTick(() => {
          this.msgDOM.scrollTop = this.msgDOM.scrollHeight
        })
      })
    },
    computed: {
      ...mapGetters([
        'getUserinfo',
        'getRobotinfo',
        'getRobotGreetMsg'
      ])
    },
    components: {
      MyMsg,
      OtherMsg
    },
    methods: {
      InitRobot() {
        const robotMsg = {
          timeStamp: Date.parse(new Date()),
          userId: this.getRobotinfo.userId,
          headPic: this.getRobotinfo.headPic,
          nickname: this.getRobotinfo.nickname,
          text: this.getRobotGreetMsg
        }
        this.MsgList.push(robotMsg)
      },
      async submit() {
        const msgObj = {
          timeStamp: Date.parse(new Date()),
          userId: this.getUserinfo.userId,
          headPic: this.getUserinfo.headPic,
          nickname: this.getUserinfo.nickname,
          text: this.inputText
        }
        await this.socket.emit('robot-msg', msgObj)
        this.MsgList.push(msgObj)
        this.inputText = ''
        this.$nextTick(() => {
          this.msgDOM.scrollTop = this.msgDOM.scrollHeight
        })
      }
    }
  }
</script>
<style lang="scss" scoped>
.content {
  width: 100%;
  height: 100%;
  .msg-content {
    background: #F6F6F6;
    height: calc(100vh - 110px);
    overflow-y: scroll;
  }
  .bottom-bar {
    height: 39px;
    display: flex;
    input{
      width: 80%;
      height: 35px;
      border: none;
      border-radius: 6px;
      font-size: 22px;
    }
    .btn {
      width: 18%;
      height: 35px;
      line-height: 35px;
      text-align: center;
      border-radius: 3px;
      color: #FFF;
      padding: 2px;
    }
    .btn-default {
      @extend .btn;
      background: #ccc;
    }
    .btn-active {
      @extend .btn;
      background: #12B7F5;
    }
  }
}
</style>
