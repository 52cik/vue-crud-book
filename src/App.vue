<template>
  <div class="container">
    <div class="col-md-6 col-md-offset-3">
      <h1>vue crud book demo</h1>

      <book-list :books="books" @del-book="delBook" @update-book="updateBook"></book-list>
      <add-book :book="book" :flag="flag" @handle-book="handleBook"></add-book>
    </div>
  </div>
</template>

<script>
import BookList from './components/BookList'
import AddBook from './components/AddBook'

export default {
  components: {
    BookList,
    AddBook,
  },

  data() {
    return {
      flag: true,
      books: [
        {"id": 1, "author": "曹雪芹", "name": "红楼梦", "price": 32},
        {"id": 2, "author": "施耐庵", "name": "水浒传", "price": 30},
        {"id": "3", "author": "罗贯中", "name": "三国演义", "price": 24},
        {"id": 4, "author": "吴承恩", "name": "西游记", "price": 20}
      ],
      book: {
        author: '',
        name: '',
        price: ''
      },
      editBook: null,
    }
  },

  methods: {
    delBook(book) {
      this.books.$remove(book)
    },
    handleBook(bk) {
      if (bk.id == undefined) {
        //添加记录
        this.book.id = this.books.length + 1
        this.books.push(this.book)
        this.book = {}
      } else {
        //修改
        //this.editBook = bk
        Object.assign(this.editBook, bk)
        this.book = {}
        this.flag = !this.flag
      }
    },
    updateBook(bk) {
      this.editBook = bk
      this.book = Object.assign({}, bk)
      this.flag = !this.flag
    }
  }
}
</script>

<style>
[v-cloak] {display: none;}
</style>
