<template>
	<div class="contain">
		<router-view/>
		<div class="bottom-bar">
			<div class="left" @click="goPage('Group')">
				<div class="left-icon">
					<img src="@/assets/img/group-icon.png" alt="" width="100%" height="100%">
				</div>
				<div>聊天群</div>
				<div class="right-icon"></div>
			</div>
			<div class="center" @click="goPageReplace('Robot')">
				<div class="center-icon">
					<img src="@/assets/img/robot-icon.png" alt="" width="100%" height="100%">
				</div>
				<div>机器人</div>
			</div>
			<div class="right" @click="goPage('MsgBoard')">
				<div class="right-icon">
					<img src="@/assets/img/msg-icon.png" alt="" width="100%" height="100%">
				</div>
				<div>留言板</div>
			</div>
		</div>
	</div>
</template>

<script type="text/javascript">
import {getItem} from '@/plugin/sessionStorage-plugin.js'

export default{
  data() {
		return {
		}
	},
	created() {
		this.InitInfo()
	},
	methods: {
		InitInfo() {
			this.$store.commit('setUserinfo', getItem('userInfo'))
		},
		goPageReplace(name) {
			this.$router.replace({name: name})
		},
		goPage(name) {
			this.$router.push({name: name})
		}
	}
}
</script>
<style lang="scss" scoped>
	$white: #F5F2C7;
	$darkblue: #F5F2C7;
	$gray: #F0F0F0;
	.contain {
		width: 100%;
		height: 100%;
		.bottom-bar {
			position: absolute;
			bottom: 0;
			left: 0;
			padding: 10px;
			width: calc(100% - 24px);
			height: 50px;
			display: flex;
			border-top: 1px solid $gray;
			justify-content: space-around;
			.left-icon, .center-icon, .right-icon{
				width: 30px;
				height: 30px;
				margin: 0 auto;
			}
		}
	}
</style>
