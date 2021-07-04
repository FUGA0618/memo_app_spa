<template>
  <div class="container is-max-desktop has-background-light p-4">
    <p class="mb-2">メモ一覧</p>
    <div class="container has-background-white p-4">
      <MemoList :memos="memos" @activate-edit-mode="activateEditMode" />
      <NewMemo @register="register" />
    </div>
  </div>

  <div v-if="editFlg" class="container is-max-desktop has-background-light mt-4 p-4">
    <textarea class="textarea mb-3" rows="10" v-model="editingMemo"></textarea>

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
import MemoList from "./MemoList.vue"
import NewMemo from "./NewMemo.vue"

export default {
  name: 'Memo',
  components: {
    MemoList,
    NewMemo
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
    update () {
      localStorage.setItem(this.editingId, this.editingMemo)
      this.editingId = null
      this.editingMemo = null
      this.editFlg = false
      this.getAllMemos()
    },
    deleteMemo () {
      if (confirm('このメモを削除しますか？')) {
        localStorage.removeItem(this.editingId)
        this.editingId = null
        this.editingMemo = null
        this.editFlg = false
        this.getAllMemos()
      }
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
