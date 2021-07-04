<template>
  <button class="button is-info"
          v-if="!registerFlg"
          @click="toggleRegister">
    <span class="icon"><i class="fas fa-plus-circle"></i></span>
    <span>追加</span>
  </button>

  <div v-if="registerFlg">
    <textarea v-model="newMemo" class="textarea mb-3" rows="10"></textarea>
    <button class="button is-info" @click="register">
      <span class="icon"><i class="fas fa-plus-circle"></i></span>
      <span>登録</span>
    </button>
  </div>
</template>

<script>
export default {
  name: 'NewMemo',
  data () {
    return {
      registerFlg: false,
      newMemo: ''
    }
  },
  methods: {
    toggleRegister () {
      this.registerFlg = !this.registerFlg
    },
    register () {
      this.$emit('register', this.newMemo)
      this.newMemo = ''
      this.registerFlg = false
    }
  }
}
</script>
