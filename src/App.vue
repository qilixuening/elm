<template>
  <div id="app">
    <keep-alive>
        <router-view v-if="$route.meta.keepAlive">
            <!--这里会被缓存的视图组件，比如Home-->
        </router-view>
    </keep-alive>
    <router-view v-if="!$route.meta.keepAlive">
        <!--这里是不被缓存的视图组件，比如Edit-->
    </router-view>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {

    }
  },
  mounted () {

  }
}
</script>

<style lang="less">
</style>
