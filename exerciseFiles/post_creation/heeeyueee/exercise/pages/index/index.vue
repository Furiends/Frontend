<template>
	<view class="content">
		<view class="button-area">
			<u--text size="18px" text="取消"></u--text>
			<view class="post—button">
				<button class="btn draft">存草稿</button>
				<button  class="btn post">发布</button>
			</view>	
		</view>
		<view class="text-area">
			<u--textarea v-model="value1" placeholder="买家都关心品牌型号 入手渠道 转手原因……" ></u--textarea>
		</view>
		<view class="image-area">
			<u-upload
				:fileList="fileList3"
				@afterRead="afterRead"
				@delete="deletePic"
				name="3"
				multiple
				:maxCount="10"
				:previewFullImage="true"
				width="120"
				height="120"
			></u-upload>
		</view>
		<view class="form-area">
			<u-cell-group >
				<u-cell size="large" icon="rmb-circle-fill"  title="价格"value="0.00" isLink></u-cell>
				<u-cell size="large" icon="moments-circel-fill"  title="同步宝贝到圈子"value="更多人看到更快卖出" isLink></u-cell>
			</u-cell-group>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				fileList3: [],
				
				value1: '',
				value2:{'fontSize': '18px'}
				
			}
		},
		onLoad() {

		},
		methods: {
			deletePic(event) {
							this[`fileList${event.name}`].splice(event.index, 1)
						},
						// 新增图片
						async afterRead(event) {
							// 当设置 mutiple 为 true 时, file 为数组格式，否则为对象格式
							let lists = [].concat(event.file)
							let fileListLen = this[`fileList${event.name}`].length
							lists.map((item) => {
								this[`fileList${event.name}`].push({
									...item,
									status: 'uploading',
									message: '上传中'
								})
							})
							for (let i = 0; i < lists.length; i++) {
								const result = await this.uploadFilePromise(lists[i].url)
								let item = this[`fileList${event.name}`][fileListLen]
								this[`fileList${event.name}`].splice(fileListLen, 1, Object.assign(item, {
									status: 'success',
									message: '',
									url: result
								}))
								fileListLen++
							}
						},
						uploadFilePromise(url) {
							return new Promise((resolve, reject) => {
								setTimeout(() => {
									resolve()
								}, 800)
							})
						},

		}
	}
</script>

<style lang="scss">
	.content {
		display: flex;
		flex-direction: column;
	}

	.text-area {
		font-size: 16px;
		height: 130px;
		
	}
	.image-area{
		height: 130px;

		margin: 10px;
	}
	
	.button-area{
		display: flex;
		justify-content: space-around;
		align-items: center;
		margin: 10px;
	}
	.post—button{
		display: flex;
		justify-content: space-around;
		width: 200px;
		.btn{
			color: #8f8f94;
			border-radius: 24px;
			flex-shrink: 0;
			width: 88px;
			height: 44px;
			font-size: 16px;
		}
		.post{
			background-color: #fef16f;
		}
		.draft{
			background-color: antiquewhite;
			border: 1px #f0f0f0 solid;
			background-color: #ffffff;
		}

	}
	.form-area{
		margin: 0px 10px;
	}

</style>
