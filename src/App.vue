<template>
  <section class="hero is-info">
    <div class="hero-body">
      <p class="title">Memo App - SPA</p>
      <p class="subtitle">by Vue.js3 and Bulma</p>
    </div>
  </section>
  <section class="section">
    <Memo />
  </section>
</template>

<script>
import Memo from "./components/Memo.vue"

export default {
  name: 'App',
  components: {
    Memo
  }
}
</script>
