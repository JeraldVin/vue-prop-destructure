<template>
  <CounterComponent :count-prop="count" :counter-details-prop="counterDetails"/>
</template>

<script>
import CounterComponent from '@/components/CounterComponent.vue'
import { reactive } from '@vue/reactivity'

export default {
  name: 'App',
  components: {
    CounterComponent
  },
  setup () {
    const state = reactive({
      count: 0,
      counterDetails: {
        count: 0
      }
    })

    let { count, counterDetails } = state

    setInterval(() => {
      count++
      counterDetails.count++
    }, 1000)

    return {
      count,
      counterDetails
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
