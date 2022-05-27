<template>
  <add-book-item
    @add-book-event="AddBookItem"
    @edit-book-event="editBookItemEvent"
    :editBook="editBook"
  />
  <books
    :books="books"
    @del-book-event="deleteBookItem"
    @edit-book-event="editBookItem"
  />
</template>

<script>
import AddBookItem from "./components/AddBookItem.vue";
import Books from "./components/Books.vue";

export default {
  name: "App",
  components: {
    Books,
    AddBookItem,
  },
  data() {
    return {
      books: [
        {
          id: 1,
          title: "1000 Leagues Under the Sea",
        },
        {
          id: 2,
          title: "The Scorpion",
        },
      ],
      editBook: {
        title: "",
        id: "",
      },
    };
  },
  methods: {
    AddBookItem(newVal) {
      this.books = [...this.books, newVal];
    },
    deleteBookItem(id) {
      this.books = this.books.filter((book) => book.id !== id);
    },
    editBookItem(id) {
      var objIndex = this.books.findIndex((obj) => obj.id === id);
      this.editBook.title = this.books[objIndex].title;
      this.editBook.id = id;
    },
    editBookItemEvent(bookItem) {
      let objIndex = this.books.findIndex((obj) => obj.id === bookItem.id);
      this.books[objIndex].title = bookItem.title;
    },
  },
  mounted() {
    if (localStorage.getItem("books")) {
      this.books = JSON.parse(localStorage.getItem("books"));
    }
  },
  watch: {
    books: {
      handler() {
        localStorage.setItem("books", JSON.stringify(this.books));
      },
      deep: true,
    },
    title: {
      handler() {
        if (this.title === "") {
          this.edit = false;
        }
      },
    },
  },
};
</script>

<style>
#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>