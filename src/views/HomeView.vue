<template>
  <div class="container">
    <nav>
      <ul>
        <li v-for="(item, index) in box" :key="index">
          <a href="#" @click.prevent="goTarget(item)">{{item+1}}</a>
        </li>
      </ul>
     </nav>
    <div class="boxs" ref="boxs">
      <div class="box" :id="`item${item}`" v-for="(item, index) in box" :key="index" :ref="el => {doms[index] = el}">
        <div class="content">{{item+1}}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { onBeforeUpdate, onMounted, ref } from 'vue'
export default {
  setup () {
    const box = ref([...Array(20).keys()])
    const doms = ref([])
    const boxs = ref(null)

    onMounted(() => {
      console.log(doms.value[3])
      console.log(boxs.value)
    })
    onBeforeUpdate(() => {
      doms.value = []
    })
    const goTarget = (item) => {
      const target = document.querySelector(`#item${item}`)
      const scrollTop = target.offsetTop
      console.log('scrollTop', scrollTop)
      window.scrollTo({ top: scrollTop, behavior: 'smooth' })
    }
    return {
      box,
      boxs,
      doms,
      goTarget
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  max-width: 1024px;
  margin: 0 auto;
  overflow: hidden;
}
.boxs {
  display: flex;
  flex-wrap: wrap;
  margin: 0 -12px;
}
.box {
  width: 25%;
  padding: 0 12px;
  margin-bottom: 12px;
  box-sizing: border-box;
}
.content {
  min-height: 100px;
  background-color: #7a5f3e;
  color: #fff;
  font-size: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
}
@media (max-width: 552px) {
  .box {
    width: 50%;
  }
}
</style>
