
<script>
	export default {
		onLaunch: function() {
			console.log('App Launch1')
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
	@import "colorui/main.css";
	@import "colorui/icon.css";
	
	/* body{
		background: #fff;
	} */
	view{
		display: block;
		box-sizing: border-box;
	}
	
</style>
