<template>
  <v-main ref="main">
    <v-container fluid>
      <router-view :key="$route.path" />
    </v-container>
  </v-main>
</template>

<script>
  export default {
    name: 'DefaultView',

    mounted () {
      try {
        const main = this.$refs.main
        const mainWrap = main.$el.querySelector('.v-main__wrap')

        const unwatch = this.$watch('$route', () => {
          /* 路由变化将主程序的 scroll 拉到初始位置 */
          mainWrap.scroll(0, 0)
        })

        this.$once('hook:beforeDestroy', () => unwatch())
      } catch (e) {
        console.error(e)
      }
    },
  }
</script>

<style scoped lang="scss">
.v-main {
  height: 100vh;

  ::v-deep .v-main__wrap {
    height: 100%;
    overflow: auto;
  }
}
</style>
