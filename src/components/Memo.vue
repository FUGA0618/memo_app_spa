<template>
  <div class="container is-max-desktop has-background-light p-4">
    <p class="mb-2">メモ一覧</p>
    <div class="container has-background-white p-4">
      <MemoList :memos="memos" @activate-edit-mode="activateEditMode" />
      <NewMemo @register="register" />
    </div>
  </div>

  <MemoEditor v-if="editFlg"
              :id="editingId"
              :memo="editingMemo"
              @update="update"
              @delete-memo="deleteMemo"/>
</template>

<script>
import MemoList from "./MemoList.vue"
import NewMemo from "./NewMemo.vue"
import MemoEditor from "./MemoEditor.vue"

export default {
  name: 'Memo',
  components: {
    MemoList,
    NewMemo,
    MemoEditor
  },
  data () {
    return {
      memos: null,
      editFlg: false,
      editingMemo: null,
      editingId: null,
    }
  },
  methods: {
    getAllMemos () {
      let memos = {}
      for (let i = 0; i < localStorage.length; i++) {
        let key = localStorage.key(i)
        if (Number.parseInt(key)) {
          memos[key] = localStorage.getItem(key)
        }
      }
      this.memos = memos
    },
    register (content) {
      let nextId = Object.keys(this.memos)
      nextId = Math.max(...nextId) + 1
      localStorage.setItem(`${nextId}`, content)
      this.getAllMemos()
    },
    update (...data) {
      const [id, memo] = data
      localStorage.setItem(id, memo)
      this.editFlg = false
      this.editingId = null
      this.editingMemo = null
      this.getAllMemos()
    },
    deleteMemo (id) {
      localStorage.removeItem(id)
      this.editFlg = false
      this.editingId = null
      this.editingMemo = null
      this.getAllMemos()
    },
    activateEditMode (...args) {
      const [id, memo] = args
      this.editFlg = true
      this.editingId = id
      this.editingMemo = memo
    }
  },
  mounted() {
    this.getAllMemos()
  }
}
</script>
