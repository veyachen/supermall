<template>
  <div class="goods-info" v-if="Object.keys(detailInfo).length !== 0">
    <div class="info-desc clear-fix">
      <div class="start"></div>
      <div class="desc">{{ detailInfo.desc }}</div>
      <div class="end"></div>
    </div>
    <div v-for="item in detailInfo.detailImage">
      <!-- <div class="info-key">{{ detailInfo.detailImage[0].key }}</div> -->
      <div class="info-key">{{ item.key }}</div>
      <div class="info-list">
        <!-- <img
          v-for="(item, index) in detailInfo.detailImage[0].list"
          :key="index"
          :src="item"
          @load="imgLoad"
          alt=""
        /> -->
        <img
          v-for="(item, index) in item.list"
          :key="index"
          :src="item"
          @load="imageLoad"
          alt=""
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "DetailGoodsInfo",
  props: {
    detailInfo: {
      type: Object,
      default() {
        return {};
      }
    }
  },
  data() {
    return {
      counter: 0,
      imagesLength: 0
    };
  },
  methods: {
    imageLoad() {
      // 监听是否所有的图片都加载完了
      // if (++this.counter === this.imagesLength) {
      this.$emit("detailImageLoad");
      // }
    }
  },
  watch: {
    // watch 监听数据的变化
    detailInfo() {
      this.imagesLength = this.detailInfo.detailImage[0].list.length;
    }
  }
};
</script>
<style scoped>
.goods-info {
  padding: 20px 0;
  border-bottom: 5px solid #f2f5f8;
  /* background-color: #fff; */
}

.info-list img {
  width: 100%;
}
</style>
