<template>
  <div id="app">
    Clicked: {{ $store.state.count }} times, count is {{ evenOrOdd }}.
    <button @click="increment">+</button>
    <button @click="decrement">-</button>
    <button @click="incrementIfOdd">Increment if odd</button>
    <button @click="incrementAsync">Increment async</button>
  </div>
</template>

<script type="text/babel">
  import Vue from 'vue'
  import Vuex from 'vuex'
  import { mapGetters, mapActions } from 'vuex'

  Vue.use(Vuex)

  const store = new Vuex.Store({
    state: {
      count: 0
    },
    mutations: {
      increment (state) {
        state.count++
      },
      decrement (state) {
        state.count--
      }
    },
    actions: {
      increment: ({ commit }) => commit("increment"),
      decrement: ({ commit }) => commit("decrement"),
      incrementIfOdd ({commit, state}) {
      if ((state.count + 1)%2 == 0) {
        commit("increment")
      }
    },
      incrementAsync ({ commit }) {
        return new Promise((resole, reject) => {
          setTimeout(() => {
            commit("increment")
            resole()
          }, 1000)
        })
      }
    },
    getters: {
      evenOrOdd: state => state.count%2==0?"even":"odd"
    }
  })

  export default {
    computed: mapGetters([
      'evenOrOdd'
    ]),
    methods: mapActions([
      'increment',
      'decrement',
      'incrementIfOdd',
      'incrementAsync'
    ]),
    store
  }
</script>
