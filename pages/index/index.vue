<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text><br/>
            <button @click="changTitle">{{butval}}</button>
			 <button @click="reChangeTitle">{{butval}}</button>
		</view>
	</view>
</template>

<script setup>
	import {ref} from "vue"
	let title= ref("你好！");
	let butval=ref("这个是按钮");
	function  changTitle(){
		title.value="改变了title";
	}
	function reChangeTitle(){
		title.value="你好";
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
