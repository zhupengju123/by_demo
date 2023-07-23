<template>
	<view class="content">
		<!-- {{List}} -->
		<text class="title">商品列表</text>
		<view class="box">
			<view class="li" @click="goDel(item.Id)" v-for="item in List">
				<image class="img" :src="item.imageUrl" mode=""></image>
				<text class="price">{{item.priceStr}}元</text>
				<text class="li_title">{{item.title}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				List: []
			};
		},
		methods: {
			getOutInfo() {
				return new Promise((resolve, reject) => {
					uni.request({
						url: `http://192.168.43.24:9527/api/goodList`,
						method: "GET",
						data: {
							page: 1
						},
						success: (res) => {

							resolve(res.data); // 千万别忘写！！！
						},
						fail: (err) => {
							reject('err')
						}
					})
				})
			},

			goDel(id) {
				console.log(id);
				
				
				uni.navigateTo({
					url: `../detail/detail?id=${id}`
				});
			}



			// async getList() {
			// 	await this.getOutInfo()
			// }
		},


		beforeMount() {
			// this.getList()

		},
		onLoad() {
			(async () => {
				await this.getOutInfo().then(res => {

					this.List = res

				})
			})()

		}
	}
</script>

<style>
	.content {
		width: 100%;

	}

	.title {
		width: 100%;
		display: inline-block;
		font-size: 20px;
		font-weight: bold;
		text-align: center;
	}

	.box {
		width: 100%;

		display: flex;
		flex-wrap: wrap;
		text-align: center;
		justify-content: space-around;
	}

	.li {

		width: 150px;
		height: 260px;
		display: flex;
		flex-wrap: wrap;
		margin-top: 10px;
		border: 2px solid rebeccapurple;

	}

	.img {
		width: 90%;
		height: 200px;
		margin: 0 auto;
		border-bottom: 1px dashed orangered;
	}

	.li_title {
		color: gray;
		font-size: 1rem;
		padding-left: 0.5rem;
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
		-o-text-overflow: ellipsis;
	}

	.price {
		padding-left: 0.5rem;
		font-size: 1.2rem;
		color: red;
	}
</style>