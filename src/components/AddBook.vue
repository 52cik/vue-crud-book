<template>
  <div id="add-book">
    <legend>添加书籍</legend>
    <div class="form-group">
      <label>书名</label>
      <input type="text" class="form-control" v-model="book.name">
    </div>
    <div class="form-group">
      <label>作者</label>
      <input type="text" class="form-control" v-model="book.author">
    </div>
    <div class="form-group">
      <label>价格</label>
      <input type="text" class="form-control" v-model="book.price">
    </div>
    <template v-if="flag">
      <button class="btn btn-primary btn-block" @click="handleBook(book)">添加</button>
    </template>
    <template v-else="flag">
      <button class="btn btn-primary btn-block" @click="handleBook(book)">修改</button>
    </template>
  </div>
</template>

<script>
export default {
  props: ['book', 'flag'],

  methods: {
    handleBook(bk) {
      if (bk.name == '' || bk.author == '' || bk.price == '') {
        alert('请填写完整');
        return;
      }

      this.$dispatch('handle-book', bk)
    }
  }
}
</script>
