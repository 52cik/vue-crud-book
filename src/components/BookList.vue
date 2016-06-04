<template>
  <table class="table table-hover" v-cloak>
    <thead>
      <tr>
        <th class="text-right" @click="sortBy('id')">序号</th>
        <th class="text-right" @click="sortBy('name')">书名</th>
        <th class="text-right" @click="sortBy('author')">作者</th>
        <th class="text-right" @click="sortBy('price')">价格</th>
        <th class="text-right">操作</th>
      </tr>
    </thead>

    <tbody>
      <tr v-for="book in books | orderBy sortparam sortorder">
        <td class="text-right">{{book.id}}</td>
        <td class="text-right">{{book.name}}</td>
        <td class="text-right">{{book.author}}</td>
        <td class="text-right">{{book.price}}</td>
        <td class="text-right">
          <button type="button" class="btn" :class="$index % 2 ? 'btn-danger' : 'btn-success' " @click="delBook(book)">删除</button>
        </td>
        <td class="text-right">
          <button type="button" class="btn" :class="$index % 2 ? 'btn-danger' : 'btn-success' " @click="updateBook(book)">修改</button>
        </td>
      </tr>
    </tbody>
  </table>

  <h4>总价: {{sum}}</h4>
</template>

<script>
export default {
  props: ['books'],

  data() {
    return {
      sortparam: '',
      sortorder: 1,
    }
  },

  computed: {
    sum() {
      let totalPrice = 0

      this.books.forEach(el => {
        totalPrice += Number(el.price)
      })

      return totalPrice
    }
  },

  methods: {
    sortBy(sortparam) {
      if (sortparam == this.sortparam) {
        this.sortorder = -this.sortorder // 逆序排列
        return
      }

      this.sortparam = sortparam
      this.sortorder = 1 // 默认正序
    },

    delBook(bk) {
      this.$dispatch('del-book', bk)
    },

    updateBook(bk) {
      this.$dispatch('update-book', bk)
    },
  },
}
</script>
