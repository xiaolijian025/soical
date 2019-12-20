<template>
	<view class="container">
		<view class="user-section">
			<image class="bg" src="/static/my/user-bg.jpg"></image>
			<view class="user-info-box">
				<view class="portrait-box">
					<image class="portrait" :src="loginStatus ? userInfo.avatar : '/static/my/missing-face.png'"></image>
				</view>
				<view class="info-box">
					<text class="username" @click="openLogin">{{loginStatus ? userInfo.nickname : '登录/注册'}}</text>
				</view>
			</view>
		</view>
		<view class="p-3" v-if="loginStatus">
			<button type="default" class="bg-white" @click="logoutEvent">退出登录</button>
		</view>
	</view>
</template>

<script>
	import { mapMutations,mapState } from 'vuex'
	export default {
		data() {
			return {
				
			}
		},
		computed: {
			...mapState({
				loginStatus:state=>state.user.loginStatus,
				userInfo:state=>state.user.userInfo,
				token:state=>state.user.token
			})
		},
		methods: {
			...mapMutations(['logout']),
			// 退出登录
			logoutEvent(){
				this.$H.post('/logout',{},{
					token:this.token
					// toast:false
				}).then(res=>{
					this.logout();
					uni.showToast({
						title: '退出成功',
						icon: 'none'
					});
					uni.navigateBack({
						delta: 1
					});
				})
			},
			openLogin(){
				if (!this.loginStatus) {
					uni.navigateTo({
						url: '/pages/login/login',
					});
				}
			},
			
		}
	}
</script>

<style lang='scss'>
%flex-center {
	 display:flex;
	 flex-direction: column;
	 justify-content: center;
	 align-items: center;
	}
	%section {
	  display:flex;
	  justify-content: space-around;
	  align-content: center;
	  background: #fff;
	  border-radius: 10rpx;
	}

	.user-section{
		height: 320rpx;
		padding: 100rpx 30rpx 0;
		position:relative;
		.bg{
			position:absolute;
			left: 0;
			top: 0;
			width: 100%;
			height: 100%;
			filter: blur(1px);
			opacity: .7;
		}
	}
	.user-info-box{
		height: 180rpx;
		display:flex;
		align-items:center;
		position:relative;
		z-index: 1;
		.portrait{
			width: 100rpx;
			height: 100rpx;
			border:5rpx solid #fff;
			border-radius: 50%;
		}
		.username{
			font-size: $font-lg + 6rpx;
			color: #303133;
			margin-left: 20rpx;
		}
	}

	

</style>
