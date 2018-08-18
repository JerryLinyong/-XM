<template>
  <div>
    <v-header :seller='seller' :description='description' @show='showMore'></v-header>
    <ul class='sectionBox'>
      <li :style="{'color': colorOne}" @click="component='form-one';colorOne='red';colorTwo='black';colorThree='black'">商品</li>
      <li :style="{'color': colorTwo}" @click="component='form-two';colorOne='black';colorTwo='red';colorThree='black'">评价</li>
      <li :style="{'color': colorThree}" @click="component='form-three';colorOne='black';colorTwo='black';colorThree='red'">商家</li>
    </ul>
    <component :is="component" class='main'  :data='data' @price='changePrice' @closeCar='closeCar' :isShow='isShow' :ratings='data.ratings'></component>
    <v-footer :price = price :buyNum = num @showCar='showCar'></v-footer>
    <div class="moredetail" v-if="show == 1" @click="show=false">
      <h1 class='detailInfo'>IF YOU WANT TO KNOW MORE</h1>
      <h2 class='detailInfo'>CONTACT ME</h2>
      <h2><a href="https://jerrylinyong.github.io/--movie/movie#">豆瓣电影</a></h2>
      <h2><a href="https://jerrylinyong.github.io/-byjerry/music#">音乐播放器</a></h2>
      <span class='close' @click='show = false'>X</span>
    </div>
  </div>
</template>

<script>
import header from './components/header/header'
import formOne from './components/goods/goods'
import formTwo from './components/ratings/ratings'
import formThree from './components/seller/seller'
import footer from './components/footer/footer'
export default {
  components: {
    'v-header': header,
    'form-one': formOne,
    'form-two': formTwo,
    'form-three': formThree,
    'v-footer': footer
  },
  data () {
    return {
      seller: '',
      description: '',
      data: '',
      component: 'form-one',
      show: '0',
      'colorOne': 'red',
      'colorTwo': '',
      'colorThree': '',
      price: 0,
      num: 0,
      isShow: false
    }
  },
  created () {
    this.$http.get('https://easy-mock.com/mock/5b5b24f0fbbb0c35ff88bf73/e').then((data) => {
      this.seller = data.body.seller
      this.description = data.body.seller.supports[0].description
      this.data = data.body
    }).catch(() => {
      console.log('erro')
    })
  },
  methods: {
    showMore () {
      this.show = '1'
      console.log(this.show)
    },
    changePrice (getPrice, getNum) {
      this.price = getPrice
      this.num = getNum
    },
    closeCar () {
      this.isShow = false
    },
    showCar () {
      this.isShow = !this.isShow
    }
  }
}
</script>

<style>
  .sectionBox {
    list-style: none;
    display: flex;
    margin: 0;
    padding: 5px 0;
    height: 30px
  }
  li {
    display: inline-block;
    flex: 1;
    height: 20px;
    padding: 5px;
    text-align: center
  }
  .moredetail {
    position: absolute;
    width: 100vw;
    height: 100vh;
    background: rgba(0,0,0,0.8);
    top: 0;
    text-align: center
  }
  .close {
    position: absolute;
    display:inline-block;
    bottom: 5px;
    left: calc(50vw - 10px);
    font-size: 30px;
    color: white
  }
  .detailInfo {
    color: white
  }
</style>
