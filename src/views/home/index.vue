<template>
  <div class="home-container">
    <head-top signin-up='home'>
      <template #logo>
        <span
          class='head_logo'
          @click='reload'
        >
          ele.me
        </span>
      </template>
    </head-top>
    <nav class="city_nav">
      <div class="city_tip">
        <span>当前定位城市：</span>
        <span>定位不准时，请在城市列表中选择</span>
      </div>
      <router-link
        :to="'city/'+guessCity"
        class="guess_city"
      >
        <span>{{ guessCity }}</span>
        <svg class="arrow_right">
          <use xlink:href="#arrow-right" />
        </svg>
      </router-link>
    </nav>
    <section id="hot_city_container">
      <h4 class="city_title">热门城市</h4>
      <ul class="citylistul clear">
        <router-link
          tag="li"
          v-for="city in hotcity"
          :key="city.id"
          :to="'/city/'+city.id"
        >
          {{ city.name }}
        </router-link>
      </ul>
    </section>
  </div>
</template>

<script>
import headTop from '@/components/head.vue'
import {
  cityGuess,
  hotcity,
  groupcity
} from '@/api/getData'

export default {
  name: 'HomeIndex',
  props: {},
  data () {
    return {
      guessCity: '', // 当前城市
      guessCityId: '', // 当前城市id
      hotCities: [], // 热门城市泪飙
      groupCites: {} // 所有城市列表
    }
  },
  components: {
    headTop
  },
  mounted () {
    this.getGuessCity()
    this.getHotCity()
    this.getGroupCity()
  },
  methods: {
    async getGuessCity () {
      const { name, id } = await cityGuess()
      this.guessCity = name
      this.guessCityId = id
    },
    async getHotCity () {
      this.hotCities = await hotcity()
    },
    async getGroupCity () {
      this.groupCites = await groupcity()
    },
    reload () {
      window.location.reload()
    }
  }
}
</script>

<style lang="less" scoped>
  .head_logo {
    left: 0.4rem;
    font-weight: 400;
    font-size: 0.7rem;
    color: #fff;
    width: 2.3rem;
    height: 0.7rem;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
  }
  .city_nav {
    padding-top: 2.35rem;
    border-top: 1px solid #e4e4e4;
    background-color: #fff;
    margin-bottom: 0.4rem;
    .city_tip {
      display: flex;
      justify-content: space-between;
      line-height: 1.45rem;
      padding: 0 0.45rem;
      span:nth-of-type(1) {
          font-size: 0.55rem;
          color: #666;
      }
      span:nth-of-type(2) {
          font-weight: 900;
          font-size: 0.475rem;
          color: #9f9f9f;
      }
    }
    .guess_city {
      display: flex;
      justify-content: space-between;
      align-items: center;
      height: 1.8rem;
      padding: 0 0.45rem;
      border-top: 1px solid #e4e4e4;
      border-bottom: 2px solid #e4e4e4;
      font: 0.75rem/1.8rem 'Microsoft YaHei';
      span:nth-of-type(1) {
        color: #3190e8;
      }
      .arrow_right {
        width: 0.6rem;
        height: 0.6rem;
        fill: #999;
      }
    }
  }
  #hot_city_container {
    background-color: #fff;
    margin-bottom: 0.4rem;
  }
  .citylistul {
    li {
      float: left;
      text-align: center;
      color: #3190e8;
      border-bottom: 0.025rem solid #e4e4e4;
      border-right: 0.025rem solid #e4e4e4;
      width: 25%;
      height: 1.75rem;
      font: 0.6rem/1.75rem 'Microsoft YaHei';
    }
    li:nth-of-type(4n) {
      border-right: none;
    }
  }
  .city_title {
    color: #666;
    font-weight: 400;
    text-indent: 0.45rem;
    border-top: 2px solid #e4e4e4;
    border-bottom: 1px solid #e4e4e4;
    font: 0.55rem/1.45rem 'Helvetica Neue';
    span {
      font-size: 0.475rem;
      color: #999;
    }
  }
</style>
