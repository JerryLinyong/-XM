<template>
  <div class="footer">
    <span class='buyNum' v-show='buyNum'>{{buyNum}}</span>
    <div class='carControl'>
      <span @click='showCar()' class='iconfont shopCar icon-gouwuche' :style='{background: activeColor}'></span>
    </div>
    <span class='totalPrice'>￥{{price}}</span>
    <span class='deliPrice'>另需配送费￥4元</span>
    <span class='startPrice' :style='{background: activeColor}'>￥20起送</span>
  </div>
</template>

<script>
export default {
  props: ['price', 'buyNum'],
  data () {
    return {
    }
  },
  computed: {
    activeColor () {
      if (this.price >= 20) {
        return 'hsl(211, 92%, 36%)'
      }
    }
  },
  created () {
  },
  methods: {
    showCar () {
      this.$emit('showCar')
    }
  }
}
</script>

<style scoped lang=stylus>
  span {
    display: inline-block
  }
  .footer {
    position: absolute;
    bottom: 0;
    width: 100%;
    height: 45px;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    background: rgb(19,19,19);
    color: rgb(150,150,150)
  }
  .carControl {
    position: absolute;
    bottom: 10px;
    left: 20px;
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: rgb(19,19,19);
    border-radius: 25px
  }
  .shopCar {
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: grey;
    border-radius: 25px;
    font-size: 25px;
    color: black
  }
  .startPrice {
    width: 120px;
    padding: 12px 0;
    text-align: center;
    background: rgba(80,80,80,0.7);
    border-radius: 5px
  }
  .deliPrice {
    width: 150px
  }
  .totalPrice {
    width: 70px;
    font-size: 20px
  }
  .buyNum
    position absolute
    top -20px
    font-size 15px
    color white
    left 60px
    background red
    height 20px
    width 40px
    border-radius 10px
    text-align center
</style>
