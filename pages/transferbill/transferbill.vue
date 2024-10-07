<template>
	<!-- 文本框  输入数据-->
	<view>
		<view class="uni-input-data">
			<input placeholder="请输入金额" type="number" v-model="inputval" />
		</view>
		<!-- 下垃框 选择转账方式  微信 银行卡-->
		<view class="uni-select-ways">
			<picker :range="pickRange" :value="selectval" @change="onPickerchange">
				<view>当前选择：{{selectval}}</view>
			</picker>
		</view>
		<!-- 按钮 执行添加数据到数据库中 -->
		<view class="uni-button-change">
			<button @click="addData">提交</button>
		</view>
	</view>
	<view>
		<!-- 提示信息弹窗 -->
		<uni-popup ref="alertmegRef" type="message" >
			<uni-popup-message :type="msgType" :message="messageText" :duration="2000" ></uni-popup-message>
		</uni-popup>
	</view>

	<!-- 表格主体 -->
	<scroll-view scroll-y>
		<uni-table border stripe emptyText="暂无更多数据">
			<uni-th align="center">时间</uni-th>
			<uni-th align="center">金额</uni-th>
			<uni-th align="center">转账方式</uni-th>
			<uni-tr v-for="(val,key,index) in bill" :key="index">
				<uni-td>{{val.time}}</uni-td>
				<uni-td>{{val.amount}}</uni-td>
				<uni-td>{{val.way}}</uni-td>
			</uni-tr>
		</uni-table>
	</scroll-view>
</template>

<script setup>
	import {
		ref,
		reactive
	} from "vue"
	const bill = reactive([{
		time: "2024-10-05 13:56",
		amount: 1345,
		way: "微信"
	}, {
		time: "2024-10-04 14:56",
		amount: 2000,
		way: "微信"
	}, {
		time: "2024-10-03 15:56",
		amount: 3000,
		way: "转账"
	}, {
		time: "2024-10-01 13:56",
		amount: 5000,
		way: "微信"
	}, {
		time: "2024-10-05 13:56",
		amount: 1000,
		way: "微信",
	}]);
	let pickRange = ['金', '英'];
	let inputval = ref("");
	let selectval = ref("");
	let msgType = ref("");
	let messageText = ref("");
	let alertmegRef =ref(null);
	function onPickerchange(e) {
		const index = e.detail.value; //获取索引
		selectval.value = pickRange[index];
	}

	function addData() {
		if (inputval.value === "" || selectval.value === "") {
			msgType.value = "error";
			messageText.value = "请输入！";
			alertmegRef.value.open();
			return;
		}
		bill.push({
			time: new Date().toISOString(),
			amount: inputval.value,
			way: selectval.value
		});
		inputval.value = 0;
		selectval.value = "";
		msgType.value = "success";
		messageText.value = "添加成功！";
		alertmegRef.value.open();
	}
</script>

<style>

</style>