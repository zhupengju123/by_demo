<template>
	<view class="box">
		<view class="li" v-for="item in List">
			<image :src="item.imageUrl" mode=""></image>
			<text class="title">{{item.title}}</text>
			<text class="salePoint">{{item.addressName}}</text>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				Id: '',
				List: []
			}

		},
		methods: {
			getDel(id) {
				return new Promise((resolve, reject) => {
					uni.request({
						url: `http://192.168.43.24:9527/api/detail`,
						method: "GET",
						data: {
							goodId: id
						},
						success: (res) => {

							resolve(res.data); // 千万别忘写！！！
						},
						fail: (err) => {
							reject('err')
						}
					})
				})

			}
		},
		onLoad(option) {
			(async () => {
				await this.getDel(option.id).then(res => {
					console.log(res);
					this.List = res

				})
			})()
		}
	}
</script>

<style>
	.li {
		margin: 0 auto;
		width: 300px;
		height: 350px;
		border: 1px solid red;
		display: flex;
		flex-wrap: wrap;

	}

	.li image {
		width: 260px;
		height: 260px;
		padding-left: 20px;
		border-bottom: 1px solid orange;

	}

	.salePoint {
		font-size: 1.2rem;
		color: orange;
	}
</style>