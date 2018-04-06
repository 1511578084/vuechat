<template>
  <div>
    <drop-list :config="configData" ref="droplist"></drop-list>
    <div class="top">
      <div class="head-pic">
        <img :src="getUserinfo.headPic" alt="headpic" width="100%" height="100%"/>
      </div>
      <div class="title">聊天群</div>
      <div class="right-icon" @click="showDropList"></div>
    </div>
    <div class="room-list">
        <div class="room-item" @click="EnterRoom('room1')">
          <div class="left-icon">
            <img src="@/assets/img/heart-icon.png" alt="" width="100%" height="100%"/>
          </div>
          <span>单身交友群</span>
        </div>
        <div class="room-item" @click="EnterRoom('room2')">
          <div class="left-icon">
            <img src="@/assets/img/game-icon.png" alt="" width="100%" height="100%"/>
          </div>
          <span>游戏交友群</span>
        </div>
        <div class="room-item" @click="EnterRoom('room3')">
          <div class="left-icon">
            <img src="@/assets/img/chat-icon.png" alt="" width="100%" height="100%"/>
          </div>
          <span>闲聊交友群</span>
        </div>
      </div>
  </div>
</template>
<script type="text/javascript">
import {mapGetters} from 'vuex'
import DropList from '@/components/DropList'
export default{
  data() {
    return {
      configData: {
        position: {
          top: '60px',
          right: '10px'
        },
        width: '40%',
        list: [
          {text: '修改资料', action: this.updateUserInfo},
          {text: '更换主题', action: this.updateTheme},
          {text: '退出账号', action: this.signOut}
        ]
      }
    }
  },
  mounted() {
  },
  computed: {
    ...mapGetters([
      'getUserinfo'
    ])
  },
  components: {
    DropList
  },
  methods: {
    EnterRoom(room) {
      this.$router.push({name: 'Chat', query: {room: room}})
    },
    showDropList() {
      this.$refs.droplist.show()
    },
    updateUserInfo() {
      console.log(123)
    },
    updateTheme() {
      console.log(123)
    },
    signOut() {
      this.$router.replace({name: 'Login'})
    }
  }
}
</script>
<style lang="scss" scoped>
  $darkblue: #12B7F5;
  $gray: #F0F0F0;
  $white: #FFF;
  .top {
    height: 50px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    background: $darkblue;
    .head-pic {
      width: 42px;
      height: 42px;
      margin-left: 10px;
      img {
        border-radius: 50%;
      }
    }
    .title {
      font-size: 20px;
      color: $white;
    }
    .right-icon {
      width: 32px;
      height: 32px;
      margin-right: 15px;
      background: url('../assets/img/set-icon.png') no-repeat center / 100%;
    }
  }
  .room-list {
      .room-item {
        height: 50px;
        display: flex;
        align-items: center;
        font-size: 20px;
        color: $darkblue;
        border-bottom: 1px solid $gray;
        padding: 0 20px;
        .left-icon{
          width: 35px;
          height: 35px;
        }
        span{
          margin-left: 30px;
        }
      }
    }
</style>
