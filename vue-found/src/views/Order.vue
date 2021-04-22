/* eslint-disable no-unused-expressions */
<template>
    <div>
        <div class="left">
            左侧是下单部分
            <ul>
                <li v-for="(item,index) in lists" :key="'order'+index">
                    <span>{{item.name}} - {{item.price}}</span>
                    <button type="button" @click="minus(item,index)"> - </button>
                    <span>{{typeof item.num === 'undefined'? 0 : item.num}}</span>
                    <button type="button" @click="add(item,index)"> + </button>
                </li>
            </ul>
        </div>
        <div class="right">
            计算的部分
            <ul>
                <li v-for="(item,index) in orders" :key="'order'+index">
                    菜品名称：{{item.name}} - 菜品单价{{item.price}} - 单项总价{{item.price * item.num}}
                </li>
            </ul>
            <p>菜单总价：{{total}}</p>
        </div>
    </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars
import _ from 'lodash'
export default {
  name: 'order',
  data () {
    return {
      lists: this.$store.state.lists
    }
  },
  computed: {
    orders () {
      const a = _.filter(this.lists, (item) => { return typeof item.num !== 'undefined' && item.num > 0 })
      return a
    },
    total () {
      let sum = 0
      _.each(this.orders, (item) => {
        sum += item.price * item.num
      })
      return sum
    }
  },
  methods: {
    minus (item, index) {
      if (typeof item.num === 'undefined') {
        item.num = 0
      }
      item.num--
      if (item.num < 0) {
        item.num = 0
      }
      this.$set(this.lists, index, item)
    },
    add (item, index) {
      if (typeof item.num === 'undefined') {
        item.num = 0
      }
      item.num++
      if (item.num > 100) {
        item.num = 100
      }
      this.$set(this.lists, index, item)
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
