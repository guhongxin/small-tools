<template>
	<view>
		<text @click="handClick">子组建</text>
	</view>
</template>

<script>
	export default {
		methods: {
			handClick() {
				console.log('子组件')
			}
		}
	}
</script>

<style>
</style>
