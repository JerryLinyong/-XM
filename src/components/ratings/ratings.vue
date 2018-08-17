<template>
  <div class="seller">
    <div class='commonJ' :style='{height: (90-top+"px")}'>
      <div class="mainscore">
        <div class="score1">{{data.seller.score}}</div>
        <div>综合评分</div>
        <div>高于周边商家{{data.seller.rankRate}}</div>
      </div>
      <div class="otherScore">
        <div>服务态度
          <img src="./star36_on@2x.png" alt="#" width="15px" v-for='star in Math.floor(data.seller.serviceScore)'>
          <img src="./star36_off@2x.png" alt="#" width="15px" v-for='star in (5-Math.floor(data.seller.serviceScore))'>
          {{data.seller.serviceScore}}</div>
        <div>美食评论
          <img src="./star36_on@2x.png" alt="#" width="15px" v-for='star in Math.floor(data.seller.foodScore)'>
          <img src="./star36_off@2x.png" alt="#" width="15px" v-for='star in (5-Math.floor(data.seller.foodScore))'>
          {{data.seller.foodScore}}</div>
        <div>送达时间&emsp;&emsp;&emsp;&emsp;{{data.seller.deliveryTime}}分钟</div>
      </div>
    </div> <div class="button">
      <span class="allS" :class='{colorAct:isA0}' @click='isShow = -1;isA0=1;isA1=0;isA2=0'>全部{{all}}</span>
      <span class="satisfy" :class='{colorAct:isA1}' @click='isShow = 1;isA1=1;isA2=0;isA0=0'>满意{{satisfy}}</span>
      <span class="disatisfy" :class='{colorAct:isA2}' @click='isShow = 0;isA2=1;isA1=0;isA0=0'>不满意{{disatisfy}}</span>
    </div>
    <div class='commonP' @scroll='hideJudge()'>
      <div class="personJud" v-for='(person,index) in ratings' :key='index' v-if='isShow === person.rateType || isShow === -1'>
        <div class="customerP">
          <img :src="person.avatar" alt="no" width="30px" height="30px">
        </div>
        <div class="judInfo">
          <div class="user">
            <span class="userName">{{person.username}}</span>
            <span class="judgeTime"> {{new Date(ratings[0].rateTime).toLocaleDateString().replace(/\//g, "-") + ' ' + new Date(ratings[0].rateTime).toTimeString().substr(0, 8)}}</span>
          </div>
          <div class="judStar">
            <img src="./star36_on@2x.png" alt="#" width="15px" v-for='star in person.score'>
            <img src="./star36_off@2x.png" alt="#" width="15px" v-for='star in (5-person.score)'>
            <span>{{person.deliveryTime}}分钟送达</span>
          </div>
          <div class="comment">
            {{person.text}}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['data', 'ratings'],
  data () {
    return {
      all: 0,
      satisfy: 0,
      disatisfy: 0,
      isShow: -1,
      isA0: 1,
      isA1: 0,
      isA2: 0,
      top: 0
    }
  },
  methods: {
    hideJudge () {
      this.top = document.querySelector('.commonP').scrollTop/2
      if (this.top > 90) {
        this.top = 90
      }
    }
  },
  mounted () {
    var _this = this
    this.ratings.forEach(function (rate) {
      _this.all += 1
      if (rate.rateType === 0) {
        _this.disatisfy += 1
      } else {
        _this.satisfy += 1
      }
    })
  }
}
</script>

<style scoped lang="stylus">
  .commonP
    height 400px
    overflow auto
  .personJud
    display flex
    margin 14px 0
  .customerP
    margin 0 20px
    img
      border-radius 16px
  .judInfo
    flex 1
    margin-right 10px
    font-size 14px
    .user
      display flex
      justify-content space-between
  .judStar
    margin 8px 0 16px 0
  .comment
    font-size 15px
  .button
    padding 10px 0
    span
      padding 4px
      margin 0 8px
      color grey
      border 1px solid black
  .colorAct
    color white
    background #55a8ff
  .commonJ
    display flex
    margin 0px 20px
    justify-content space-between
    overflow hidden
  .mainscore
    text-align center
    .score1
     color orange
     font-size 30px
  .otherScore
    div
      font-size 18px
      margin 5px
</style>
