<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	/* 记得加“;”，不然不能正确引入 */
	
	@import "./common/uni.css";
	
	@import "./common/icon.css";
	
	@import "./common/animate.css"
	
</style>
