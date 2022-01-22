<template>
  <div id="app">
    <div id="nav">
      <h3>elm</h3>
    </div>
    <keep-alive>
        <router-view v-if="$router.meta.keepAlive">
            <!--这里会被缓存的视图组件，比如Home-->
        </router-view>
    </keep-alive>
    <router-view v-if="!$route.meta.keepAlive">
        <!--这里是不被缓存的视图组件，比如Edit-->
    </router-view>
  </div>
</template>

<style lang="less">
</style>
