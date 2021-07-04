<template>
  <ul>
    <a v-for="(memo, index) in memos"
       :key="index">
      <li class="py-1">{{ memo }}</li>
    </a>
  </ul>
</template>

<script>
export default {
  name: 'MemoList',
  props: ['memos']
}
</script>
