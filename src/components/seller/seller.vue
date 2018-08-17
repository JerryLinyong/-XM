<template>
  <div class="seller">
    <div class="sellerName">
      {{data.seller.name}}
    </div>
    <div class="sellerJ">
      <img src="./star36_on@2x.png" alt="#" width="20px" v-for='star in Math.floor(data.seller.foodScore)'>
      <img src="./star36_off@2x.png" alt="#" width="20px" v-for='star in (5-Math.floor(data.seller.foodScore))'>
      <span>&emsp;月售{{data.seller.sellCount}}单</span>
    </div>
    <div class="sellerDetail">
      <div class="sellingInfo">
        <p>起送价</p>
        <p><span class="numberInfo">{{data.seller.minPrice}}</span>元</p>
      </div>
      <div class="sellingInfo">
        <p>商家配送</p>
        <p><span class="numberInfo">{{data.seller.deliveryPrice}}</span>元</p>
      </div>
      <div class="sellingInfo">
        <p>平均配送时间</p>
        <p><span class="numberInfo">{{data.seller.deliveryTime}}</span>分钟</p>
      </div>
    </div>
    <div class="bulletin">
      <h2>公告与活动</h2>
      <div class="sellerBulletin">
        {{data.seller.bulletin}}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['data'],
  data () {
    return {
    }
  },
  created () {
  }
}
</script>

<style scoped>
  .sellerName {
    font-size: 24px;
    padding: 10px 0 10px 20px
  }
  .sellerJ {
    padding: 5px 0 4px 20px;
    font-size: 16px
  }
  .sellerDetail {
    display: flex;
    justify-content: space-around;
    border-top: 1px solid rgb(184, 173, 173);
    border-bottom: 1px solid rgb(184, 173, 173);
    padding: 16px 0;
    margin: 12px 0
  }
  .numberInfo {
    font-size: 30px
  }
  .sellingInfo>p {
    text-align: center;
    margin: 0
  }
  .sellerBulletin {
    padding-left: 20px;
    color: red
  }
</style>
