<template>
  <div class="container is-max-desktop has-background-light mt-4 p-4">
    <textarea v-model="editingMemo" class="textarea mb-3" rows="10"></textarea>

    <button @click="update" class="button is-success mr-3">
      <span class="icon"><i class="fas fa-edit"></i></span>
      <span>更新</span>
    </button>

    <button @click="deleteMemo" class="button is-danger">
      <span class="icon"><i class="fas fa-trash-alt"></i></span>
      <span>削除</span>
    </button>
  </div>
</template>

<script>
export default {
  name: 'MemoEditor',
  props: ['id', 'memo'],
  data () {
    return {
      editingMemo: this.memo,
      editingId: this.id,
    }
  },
  methods: {
    update () {
      this.$emit('update', this.editingId, this.editingMemo)
      this.editingId = null
      this.editingMemo = null
    },
    deleteMemo () {
      if (confirm('このメモを削除しますか？')) {
        this.$emit('deleteMemo', this.editingId)
        this.editingId = null
        this.editingMemo = null
      }
    }
  },
  watch: {
    id: function (newId) {
      this.editingId = newId
    },
    memo: function (newMemo) {
      this.editingMemo = newMemo
    }
  }
}
</script>
