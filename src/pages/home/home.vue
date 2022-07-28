<template>
	<view class="content">
		<!-- 搜索组件 -->
    <!-- <view class="search-box">
      <my-search @click="gotoSearch"></my-search>
    </view> -->

    <!-- 轮播图的区域 -->
    <swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" :circular="true">
      <swiper-item v-for="(item, i) in swiperList" :key="i">
        <navigator class="swiper-item" :url="'/subpkg/goods_detail/goods_detail?goods_id=' + item.goods_id">
          <image :src="item.image_src"></image>
        </navigator>
      </swiper-item>
    </swiper>

	</view>
</template>

<script>
	export default {
		data() {
			return {
        swiperList: [
          {
            image_src: require('static/tab_icons/home.png')
          },
          {
            image_src: require('static/tab_icons/cate.png')
          },
          {
            image_src: require('static/tab_icons/cart.png')
          },
          {
            image_src: require('static/tab_icons/my.png')
          }
        ]  // 轮播图数据
			}
		},
		onLoad() {
      // this.getSwiperList()
		},
		methods: {
      getSwiperList() {
        debugger
        const { data: res } = uni.$http.get('/api/public/v1/home/swiperdata')
        if(res.meta.status !== 200) {
          return uni.showToast({
            title: '数据请求失败！',
            duration: 1500,
            icon: 'none'
          })
        }
        this.swiperList = res.message
      },
      gotoSearch() {

      }
		}
	}
</script>

<style lang="scss" scoped>
swiper {
 height: 330rpx;

 .swiper-item,
 image {
   width: 100%;
   height: 100%;
 }
}
</style>
