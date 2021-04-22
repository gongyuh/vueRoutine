<template>
  <div>
    <div class="home">
      {{ msg }}
    </div>
    <div class="left">
      <form v-if="isShow">
        <div class="item">
          菜品名称
          <input type="text" v-model="unit.name">
        </div>
        <div class="item">
          菜品图片
          <input type="text" v-model="unit.url">
        </div>
        <div class="item">
          菜品分类
          <input type="text" v-model="unit.type">
        </div>
        <div class="item">
          菜品单价
          <input type="text" v-model="unit.price">
        </div>
        <button type="button" @click="submit()">确定</button>
      </form>
      <div class="info" v-else>
        {{unit.name}} - {{unit.url}} - {{unit.price}} - {{unit.type}}
        <div class="ctrl">
          <button type="button" @click="add()">添加</button>
          <button type="button" @click="cancel()">取消123</button>
        </div>
      </div>
    </div>
    <div class="right">
      <ul>
        <li v-for="(item,index) in list" :key="index">
          {{item.name}} - {{item.price}} - {{item.type}}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  name: 'Home',
  data () {
    return {
      msg: 'hello world!',
      isShow: true,
      unit: {
        name: '',
        url: '',
        type: '',
        price: ''
      },
      list: []
    }
  },
  components: {},
  mounted () {
    this.list = this.$store.state.lists
  },
  methods: {
    submit () {
      this.isShow = false
    },
    add () {
      this.list.push({ ...this.unit })
      this.$store.commit('setList', this.list)
      this.unit.name = ''
      this.unit.url = ''
      this.unit.type = ''
      this.unit.price = ''
      this.isShow = true
    },
    cancel () {
      this.isShow = true
    }
  }

}
</script>

<style lang="scss">

</style>
