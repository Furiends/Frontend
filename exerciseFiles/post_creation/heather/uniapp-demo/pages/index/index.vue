<template>
  <view class="content">
    <view class="fb_tool">
      <button @click="addImages">+</button>
      <view
        class="up_img_item"
        v-for="(item, index) in chooseImgs"
        :key="index"
        @click="deleteImage(index)"
      >
        <imagesUpload :src="item"></imagesUpload>
      </view>
    </view>
    <button type="primary" @click="submit">提交</button>
  </view>
</template>

<script>
import imagesUpload from '@/components/imageUpload/imagesUpload.vue';
export default {
  components: {
    imagesUpload,
  },
  data() {
    return {
      // 被选中的图片路径 数组
      chooseImgs: [],
    };
  },
  onLoad() {},
  methods: {
    addImages() {
      uni.chooseImage({
        count: 3,
        success: (res) => {
          console.log(res);
          const tempFilePaths = res.tempFilePaths;
          tempFilePaths.forEach((path) => {
            this.chooseImgs.push(path);
          });
        },
      });
    },
    deleteImage(index) {
      this.chooseImgs.splice(index, 1);
    },
    async submit() {
      if (!this.chooseImgs.length) {
        return;
      }

      this.chooseImgs.forEach((image, index) => {
        this.uploadFiles(image[index].url);
      });
    },
    async uploadFiles(filePath) {
      await uni.uploadFiles({
        url: 'https://www.example.com/upload', //仅为示例，非真实的接口地址
        filePath,
        name: 'rrr',
        success: (uploadFileRes) => {
          console.log(uploadFileRes.data);
        },
      });
    },
  },
};
</script>

<style>
.fb_tool {
  display: flex;
  flex-wrap: wrap;
  padding-bottom: 30rpx;
}

.fb_tool button {
  margin: 0;
  width: 90rpx;
  height: 90rpx;
  font-size: 60rpx;
  padding: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 20rpx;
  margin-top: 20rpx;
  color: #ccc;
}

.fb_tool .up_img_item {
  margin-left: 20rpx;
  margin-top: 20rpx;
}
</style>
