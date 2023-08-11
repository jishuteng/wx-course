<template>
	<web-view :src="url" bindmessage="getMessage"></web-view>
</template>
 
<script>
	export default {
		data() {
			return {
				url:'http://xk.huel.edu.cn/jwglxt/xtgl/login_slogin.html',
			}
		},
		onLoad(options) {
			this.url = options.url;
		}
	}
</script>
 
<style>
 
</style>