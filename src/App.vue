<template>
  <div id="app">
    <!-- 头部内容 -->
    <v-header :seller="seller"></v-header>
    <div class="tab-wrapper">
      <tab :tabs="tabs" :initialIndex=1></tab>
    </div>
  </div>
</template>

<script>
import VHeader from 'components/v-header/v-header'
import Goods from 'components/goods/goods'
import Seller from 'components/seller/seller'
import Ratings from 'components/ratings/ratings'
import Tab from 'components/tab/tab'
import { getSeller } from 'api'
export default {
  name: 'app',
  data () {
    return {
      seller: {}
    }
  },
  created () {
    getSeller().then((seller) => {
      this.seller = seller
    })
  },
  components: {
    VHeader,
    Tab
  },
  computed: {
    tabs () {
      return [
        { label: '商品',
          component: Goods,
          data: {
            seller: this.seller
          }
        },
        { label: '评价',
          component: Ratings,
          data: {
            seller: this.seller
          }
        },
        { label: '商家',
          component: Seller,
          data: {
            seller: this.seller
          }
        }
      ]
    }
  }
}
</script>
<style lang="stylus" scoped>
#app
  .tab-wrapper
    position fixed
    top 136px
    left 0
    right 0
    bottom 0
</style>
