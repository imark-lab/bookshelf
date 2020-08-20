<template>
  <div class="search">
    <p>本を検索</p>

    <form @submit.prevent="getBooks(query)">
      <input
        type="text"
        v-model="query"
        placeholder="著者名、本のタイトルを入力"
      />
    </form>
    <ShowBooks
      v-for="book in books"
      :key="book.id"
      :img="book.volumeInfo.imageLinks.thumbnail"
      :title="book.volumeInfo.title"
      :subtitle="book.volumeInfo.subtitle"
    />
  </div>
</template>

<script>
import axios from "axios";
import ShowBooks from "./Books.vue";

export default {
  name: "BooksSearch",
  components: {
    ShowBooks,
  },
  data() {
    return {
      query: "",
      books: [],
      loading: "検索結果が表示されます",
    };
  },
  methods: {
    getBooks: async function(query) {
      const response = await axios.get(
        "https://www.googleapis.com/books/v1/volumes?q=" + query
      );
      this.books = response.data.items;
      console.log(this.books);
    },
  },
};
</script>
