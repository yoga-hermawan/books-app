<template>
  <div>
    <h2>books crud</h2>
    <div :key="book.id" v-for="book in books">
      <book-item
        :book="book"
        @del-book-item="delBookMethod"
        @edit-book-item="editBookMethod"
      />
    </div>
    <div v-if="!books.length">
      <p>No Books to Read!!</p>
    </div>
  </div>
</template>

<script>
import BookItem from "./BookItem.vue";
export default {
  components: { BookItem },
  name: "books-component",
  props: ["books"],
  methods: {
    delBookMethod(id) {
      this.$emit("del-book-event", id);
    },
    editBookMethod(id) {
      this.$emit("edit-book-event", id);
    },
  },
};
</script>