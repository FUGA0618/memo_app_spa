<template>
  <div class="container is-max-desktop has-background-light p-4">
    <p class="mb-2">メモ一覧</p>
    <div class="container has-background-white p-4">
      <MemoList :memos="memos" />
      <NewMemo @register="register" />
    </div>
  </div>

  <div class="container is-max-desktop has-background-light mt-4 p-4">
    <textarea class="textarea mb-3" rows="10"></textarea>

    <button class="button is-success mr-3">
      <span class="icon"><i class="fas fa-edit"></i></span>
      <span>編集</span>
    </button>

    <button class="button is-danger">
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
    }
  },
  mounted() {
    this.getAllMemos()
  }
}
</script>
