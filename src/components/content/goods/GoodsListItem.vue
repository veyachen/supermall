<template>
  <div class="goods-item" @click="itemClick">
    <!-- <img :src="showImage" alt="" @load="imageLoad" /> -->
    <img v-lazy="showImage" alt="" @load="imageLoad" />
    <div class="goods-info">
      <p>{{ goodsItem.title }}</p>
      <span class="price">{{ goodsItem.price }}</span>
      <span class="collect">{{ goodsItem.cfav }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "GoodsListItem",
  props: {
    goodsItem: {
      type: Object,
      default() {
        return {};
      }
    }
  },
  computed: {
    showImage() {
      return this.goodsItem.image || this.goodsItem.show.img;
    }
  },
  methods: {
    imageLoad() {
      this.$bus.$emit("itemImgLoad");
      // if (this.$route.path.indesOf("/home")) {
      //   // console.log("imageLoad");
      //   // 事件总线：和Vuex相似，是用来管理事件的
      //   this.$bus.$emit("homeItemImageLoad"); //利用事件总线发射出去一个事件
      // } else if (this.$route.path.indesOf("/detail")) {
      //   this.$bus.$emit("detailItemImageLoad");
      // }
    },
    itemClick() {
      this.$router.push("/detail/" + this.goodsItem.iid);
      // console.log(this.goodsItem.iid);
      // this.$router.push({
      //   path: "/detail",
      //   query: {}
      // });
    }
  }
};
</script>
<style>
.goods-item {
  padding-bottom: 40px;
  position: relative;

  width: 48%;
}

.goods-item img {
  width: 100%;
  border-radius: 5px;
}

.goods-info {
  font-size: 12px;
  position: absolute;
  bottom: 5px;
  left: 0;
  right: 0;
  overflow: hidden;
  text-align: center;
}

.goods-info p {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-bottom: 3px;
}

.goods-info .price {
  color: var(--color-high-text);
  margin-right: 20px;
}

.goods-info .collect {
  position: relative;
}

.goods-info .collect::before {
  content: "";
  position: absolute;
  left: -15px;
  top: -1px;
  width: 14px;
  height: 14px;
  background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
}
</style>
