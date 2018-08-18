<template>
  <div class="goods">
    <div class="menu">
      <ul class='type'>
        <li v-for='type in data.goods' :key='type.name' @click='toggleN(type.name)' class='typeName'><p>{{type.name}}</p></li>
      </ul>
    </div>
    <div class="detail" id='detail'>
      <ul class='foods'>
          <li class="typeNameTwo" v-for="typeName in data.goods" :key='typeName.name'>
            <p class="typeNameTwoP">{{typeName.name}}</p>
            <ul>
              <li class="foodType" v-for="foodType in typeName.foods" :key='foodType.name'>
                <img :src=foodType.image alt="图片错误" width='75px' height='75px'>
                <div class="typeInfo">
                  <p class="infoName">{{foodType.name}}</p>
                  <p class="infoType">{{foodType.description}}</p>
                  <p class="infoCount">月售{{foodType.sellCount}}份&nbsp;&nbsp;好评率{{foodType.rating}}%</p>
                  <p class="infoPrice">￥{{foodType.price}}</p>
                </div>
                <span v-if='buyCount[foodType.name]'>
                  <span class='iconfont icon-iconless minBtn' @click="minusOne(foodType.name),minPrice(foodType.price)">
                    <span>{{buyCount[foodType.name]}}</span>
                  </span>
                </span>
                <span class='iconfont icon-jiahao addBtn' @click="addOne(foodType.name),addPrice(foodType.price)"></span>
              </li>
            </ul>
          </li>
      </ul>
    </div>
    <div class='blurBg' v-show='isShow' @click='closeCar()'></div>
    <div class='shopcar' v-show='isShow'>
      <div class='carInfo'>
        <span>购物车</span>
        <span class='clearCar' @click='clearCar()'>清空</span>
      </div>
      <ul>
        <li class="shopcarlist" v-for="(value,key, index) in buyCount" :key='index' v-if='value'>
          <span class='goodsName'>{{key}}</span>
          <div class='shopcarInfo'>
          <span class='shopcarPrice'>￥{{price[key]}}</span>
          <span class='iconfont icon-iconless shopcarMin' @click="minusOne(key),minPrice(price[key])"><span></span></span>
          <span>{{value}}</span>
          <span class='iconfont icon-jiahao shopcarAdd' @click="addOne(key),addPrice(price[key])"></span>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  props: ['data', 'isShow'],
  data () {
    return {
      buyCount: {'皮蛋瘦肉粥': 0, '扁豆焖面': 0, '葱花饼': 0, '牛肉馅饼': 0, '招牌猪肉白菜锅贴/10个': 0, '南瓜粥': 0, '红豆薏米美肤粥': 0, '八宝酱菜': 0, '红枣山药糙米粥': 0, '糊塌子': 0, '红枣山药粥套餐': 0, 'VC无限橙果汁': 0, '娃娃菜炖豆腐': 0, '手撕包菜': 0, '香酥黄金鱼/3条': 0, '拍黄瓜': 0, '红豆薏米粥套餐': 0, '皮蛋瘦肉粥套餐': 0, '蜜瓜圣女萝莉杯': 0, '加多宝': 0, '鲜蔬菌菇粥': 0, '田园蔬菜粥': 0},
      price: {'皮蛋瘦肉粥': 10, '扁豆焖面': 14, '葱花饼': 10, '牛肉馅饼': 14, '招牌猪肉白菜锅贴/10个': 17, '南瓜粥': 9, '红豆薏米美肤粥': 12, '八宝酱菜': 4, '红枣山药糙米粥': 10, '糊塌子': 10, '红枣山药粥套餐': 29, 'VC无限橙果汁': 8, '娃娃菜炖豆腐': 17, '手撕包菜': 16, '香酥黄金鱼/3条': 11, '拍黄瓜': 9, '红豆薏米粥套餐': 37, '皮蛋瘦肉粥套餐': 31, '蜜瓜圣女萝莉杯': 6, '加多宝': 6, '鲜蔬菌菇粥': 11, '田园蔬菜粥': 10},
      Count: 0,
      num: 0,
      menueNow: 0,
      hah: true
    }
  },
  methods: {
    addOne (name) {
      this.buyCount[name] += 1
    },
    minusOne (name) {
      this.buyCount[name] -= 1
    },
    addPrice (price) {
      this.Count += price
      this.num += 1
      this.$emit('price', this.Count, this.num)
    },
    minPrice (price) {
      this.Count -= price
      this.num -= 1
      this.$emit('price', this.Count, this.num)
    },
    toggleN (name) {
      if (name === '热销榜') {
        document.querySelector('#detail').scrollTop = 0
      } else if (name === '单人精彩套餐') {
        document.querySelector('#detail').scrollTop = 1020
      } else if (name === '冰爽饮品限时特惠') {
        document.querySelector('#detail').scrollTop = 1140
      } else if (name === '精选热菜') {
        document.querySelector('#detail').scrollTop = 1250
      } else if (name === '爽口凉菜') {
        document.querySelector('#detail').scrollTop = 1570
      } else if (name === '精选套餐') {
        document.querySelector('#detail').scrollTop = 1790
      } else if (name === '果拼果汁') {
        document.querySelector('#detail').scrollTop = 2010
      } else if (name === '小吃主食') {
        document.querySelector('#detail').scrollTop = 2330
      } else if (name === '特色粥品') {
        document.querySelector('#detail').scrollTop = 2840
      }
    },
    clearCar () {
      for (var goods in this.buyCount) {
        this.buyCount[goods] = 0
        this.Count = 0
        this.num = 0
        this.$emit('price', this.Count, this.num)
      }
    },
    closeCar () {
      this.$emit('closeCar')
    }
  },
  computed: {
  },
  updated () {
    var p = document.querySelectorAll('.typeName')
    var Top
    document.querySelector('#detail').addEventListener('scroll', function () {
      Top = document.querySelector('#detail').scrollTop
      p.forEach(function (x) {
        x.classList.remove('change')
      })
      if (Top < 1010) {
        p[0].classList.add('change')
      } else if (Top < 1140 && Top >= 1020) {
        p[1].classList.add('change')
      } else if (Top < 1250 && Top >= 1140) {
        p[2].classList.add('change')
      } else if (Top < 1570 && Top >= 1250) {
        p[3].classList.add('change')
      } else if (Top < 1790 && Top >= 1570) {
        p[4].classList.add('change')
      } else if (Top < 2010 && Top >= 1790) {
        p[5].classList.add('change')
      } else if (Top < 2330 && Top >= 2010) {
        p[6].classList.add('change')
      } else if (Top < 2840 && Top >= 2330) {
        p[7].classList.add('change')
      } else if (Top >= 2840) {
        p[8].classList.add('change')
      }
    })
  }
}
</script>

<style scoped lang="stylus">
    .goods {
        position relative
        display: flex
    }
    .menu {
        width: 80px;
        height: calc(100vh - 230px);
        overflow: auto
    }
    ul {
        list-style: none;
        padding: 0;
        margin: 0;
    }
    .typeName {
        width: 80px;
        height:60px;
        padding: 0;
        font-size: 13px;
        background: rgba(100,100,100,0.1)
    }
    .typeName>p {
        width: 70px;
        margin: 0;
        margin-left: 4px;
        height: 60px;
        border-bottom: 1px solid grey;
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .detail {
        position relative
        flex: 1;
        height: calc(100vh - 230px);
        overflow: auto
    }
    .typeNameTwo {
        margin: 0;
        padding: 5px 0;
        text-align: start;
        width: 100%;
        background: rgba(100,100,100,0.1);
        border-left: 2px solid rgb(200,200,200)
    }
    .foodType {
        position: relative;
        display: flex;
        height: 100px;
        align-items: center;
        padding: 0 0 0 10px
    }
    .typeInfo {
        margin-left: 10px;
        height: 100px;
        display: flex;
        flex-direction: column;
        justify-content: center
    }
    .typeInfo p
        margin 0
        text-align start
    .infoCount
        font-size 14px
    .infoType
        width 200px
        overflow hidden
        font-size 14px
        white-space nowrap
        text-overflow ellipsis
    .infoName
        font-weight bold
        font-size 18px
    .infoPrice
        color red
        font-size 18px
        font-weight bold
    .typeNameTwoP
        margin 0
    .addBtn
    .minBtn
        position absolute
        color #027dffab
        font-size 24px
        right 5px
        bottom 5px
    .minBtn
        right 40px
        color grey
        span
            color black
            font-size 20px
            margin-left 10px
    .change
        background white
    .shopcar
        position absolute
        bottom -10px
        width 100vw
        padding-bottom 14px
        background white
    .shopcarlist
        padding 10px
        .goodsName
            margin-left 20px
            display inline-block
            width 200px
            text-align left
        .shopcarInfo
            display inline-flex
            width 160px
            justify-content space-between
        span
            font-size 22px
        .shopcarAdd
            color #55a8ff
        .shopcarPrice
            color red
        .shopcarMin
            color grey
    .blurBg
        position absolute
        bottom 0px
        width 100vw
        height 100vh
        background rgba(0,0,0,0.7)
    .clearCar
        position absolute
        right 5px
    .carInfo
        padding 10px
        border-bottom grey 1px solid
</style>
