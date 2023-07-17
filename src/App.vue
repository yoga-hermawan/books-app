<template>
  <div class="centering-div">
    <div class="card" v-for="(c, i) in company" :key="i">
      <img
        src="https://www.w3schools.com/w3images/jeans3.jpg"
        alt="Denim Jeans"
        style="width: 100%"
      />
      <h1>{{ c.name }}</h1>
      <p class="price">{{ c.username }}</p>
      <p>{{ c.company.catchPhrase }}</p>
      <p><button>Add to Cart</button></p>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
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
      company: {},
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
    getCompany() {
      console.log("jalan");
      let option = {
        methods: "GET",
        headers: {
          Authorization:
            "Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJiZWFyZXIiLCJzdWIiOjIsImlhdCI6MTY4NzA4MjgzMCwiZXhwIjoxNjg3MTY5MjMwLCJyb2xlIjoyfQ.GSIcljIa0zraSum_WvSew8-ynfNOAQsNJSCpLdk9ebE",
        },
      };
      fetch("https://jsonplaceholder.typicode.com/users", option)
        .then(function (res) {
          return res.json();
        })
        .then((resJson) => {
          let vm = this;
          vm.company = resJson;
          console.log(vm.company);
        });
    },
  },
  mounted() {
    if (localStorage.getItem("books")) {
      this.books = JSON.parse(localStorage.getItem("books"));
    }
    this.getCompany();
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

.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  max-width: 300px;
  margin: auto;
  text-align: center;
  font-family: arial;
}

.price {
  color: grey;
  font-size: 22px;
}

.card button {
  border: none;
  outline: 0;
  padding: 12px;
  color: white;
  background-color: #000;
  text-align: center;
  cursor: pointer;
  width: 100%;
  font-size: 18px;
}

.card button:hover {
  opacity: 0.7;
}

.centering-div {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  justify-content: center;
  align-items: center;
}
</style>