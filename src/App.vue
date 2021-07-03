<template>
  <section class="hero is-info">
    <div class="hero-body">
      <p class="title">Memo App - SPA</p>
      <p class="subtitle">by Vue.js3 and Bulma</p>
    </div>
  </section>

  <section class="section">

    <div class="container is-max-desktop has-background-light p-4">
      <p class="mb-2">メモ一覧</p>
      <div class="container has-background-white p-4">
        <ul>
          <a href="#"><li class="py-1">サンプルメモ１</li></a>
          <a href="#"><li class="py-1">サンプルメモ２</li></a>
          <a href="#"><li class="py-1">サンプルメモ３</li></a>
          <a href="#"><li class="py-1">サンプルメモ４</li></a>
          <a href="#"><li class="py-1">サンプルメモ５</li></a>
        </ul>
        <button class="button is-info">
          <span class="icon">
            <i class="fas fa-plus-circle"></i>
          </span>
          <span>追加</span>
        </button>
      </div>
    </div>

    <div class="container is-max-desktop has-background-light mt-4 p-4">
      <textarea class="textarea mb-3" rows="10"></textarea>

      <button class="button is-success mr-3">
        <span class="icon">
          <i class="fas fa-edit"></i>
        </span>
        <span>編集</span>
      </button>

      <button class="button is-danger">
        <span class="icon">
          <i class="fas fa-trash-alt"></i>
        </span>
        <span>削除</span>
      </button>
    </div>

  </section>
</template>

<script>
export default {
  name: 'App',
}
</script>
