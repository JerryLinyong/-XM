<template>
  <div class='header'>
    <img class="background" :src="seller.avatar" alt="网络错误">
    <div class="brandHeader">
        <img :src="seller.avatar" alt='网络出错' width="70px" height="70px">
        <span class="brandInfo">
          <div class='brandName'>
            <img src="./brand@2x.png" width='35px' height='20px'>{{seller.name}}
          </div>
          <p>{{seller.description}}/{{seller.deliveryTime}}分钟送达</p>
          <div class="discount">
           <img src="./decrease_2@2x.png" width='20px' height='20px'>
           <span>{{description}}</span>
          </div>
          <a class="detail" @click="show">5个</a>
        </span>
    </div>
    <div class="bulletin">
      <img src="./bulletin@2x.png" alt='网络出错' width="30px" height="15px">
      <span>{{seller.bulletin}}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: ['seller', 'description'],
  data () {
    return {
      color: 'red'
    }
  },
  methods: {
    show () {
      this.$emit('show')
    }
  }
}
</script>

<style scoped>
  .header {
    height: 130px;
    position:relative;
    background: rgba(0,0,0,0.5);
    color: rgba(255,255,255,0.7);
    font-weight: bold;
    overflow: hidden
  }
  .background {
    position: absolute;
    width: 100%;
    height: 100%;
    z-index: -1;
    filter: blur(3px);
  }
  .brandHeader {
    position: relative;
    display: flex;
    left: 20px;
    top: 20px;
    align-items: center
  }
  .brandHeader p {
    margin: 5px 5px;
    font-size: 15px
  }
  .brandName {
    display: flex;
    justify-content: space-between;
    color: white
  }
  .brandInfo {
    display: inline-block;
    margin-left: 30px
  }
  .detail {
    position: absolute;
    display: inline-block;
    right: 20px;
    bottom: 0px;
    width: 50px;
    text-align: center;
    border-radius: 10px;
    background: rgba(0,0,0,0.5)
  }
  .bulletin {
    display: flex;
    margin-top: 30px;
    padding: 5px 0px;
    font-size: 15px;
    align-items: center;
    background: black;
    opacity: 0.5
  }
  .bulletin > span {
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
  }
  .discount {
    display: flex
  }
  .header img {
    margin: 0 5px
  }
  .discount>span {
    font-size: 8px
  }
</style>
