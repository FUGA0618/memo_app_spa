<template>
  <ul>
    <a v-for="(memo, index) in memos"
       :key="index"
       @click="activateEditMode(index, memo)">
      <li class="py-1">{{ splitOneLine(memo) }}</li>
    </a>
  </ul>
</template>

<script>
export default {
  name: 'MemoList',
  props: ['memos'],
  methods: {
    splitOneLine (memo) {
      return memo.split('\n')[0]
    },
    activateEditMode (id, memo) {
      this.$emit('activateEditMode', id, memo)
    }
  }
}
</script>
