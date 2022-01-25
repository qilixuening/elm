<template>
  <div class="home-container">
    ELE.me
  </div>
</template>

<script>
import { cityGuess } from '@/api/getData'

export default {
  name: 'HomeIndex',
  props: {},
  data () {
    return {
      guessCity: '',
      guessCityId: ''
    }
  },
  created () {
    this.getGuessCity()
  },
  methods: {
    async getGuessCity () {
      const { name, id } = await cityGuess()
      this.guessCity = name
      this.guessCityId = id
    }
  }
}
</script>

<style lang="less" scoped>

</style>
