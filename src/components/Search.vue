<template>
  <div class="search">
    <div id="selectTab">
      <input
        class="byBook"
        type="button"
        value="本の名前で検索"
        @click="searchByBook()"
        :class="{ bookSelected: byBook }"
      />
      <input
        class="byISBN"
        type="button"
        value="ISBNコードで検索"
        @click="searchByISBN()"
        :class="{ ISBNSelected: byISBN }"
      />
    </div>

    <form @submit.prevent="getBooks(query)" v-if="byBook">
      <input
        type="text"
        v-model="query"
        placeholder="本のタイトルを入力"
        :class="{ clicked: isClicked }"
      />
    </form>
    <form @submit.prevent="getBooksByISBN(query)" v-if="byISBN">
      <input
        type="text"
        v-model="query"
        placeholder="ISBNコードを入力"
        :class="{ ISBNIsClicked: isClicked }"
      />
    </form>
    <h3>{{ message }}</h3>
    <div id="books">
      <ShowBooks
        v-for="book in books"
        :key="book.id"
        :img="book.volumeInfo.imageLinks.thumbnail"
        :title="book.volumeInfo.title"
        :authors="book.volumeInfo.authors"
        :link="book.volumeInfo.previewLink"
        :page="book.volumeInfo.pageCount"
        :lang="book.volumeInfo.language"
        :date="book.volumeInfo.publishedDate"
        :print-type="book.volumeInfo.printType"
      />
    </div>
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
      message: "検索内容を入力してください",
      isClicked: false,
      byBook: true,
      byISBN: false,
    };
  },
  methods: {
    getBooks: async function(query) {
      const response = await axios.get(
        "https://www.googleapis.com/books/v1/volumes?q=" + query
      );
      this.books = response.data.items;
      this.message = "";
      console.log(this.books);
    },
    getBooksByISBN: async function(query) {
      const response = await axios.get(
        "https://www.googleapis.com/books/v1/volumes?q=isbn:" + query
      );
      this.books = response.data.items;
      if (this.books == undefined) {
        this.message = "検索した本が存在しません。";
      } else {
        this.message = "";
      }
      console.log(this.books);
    },
    searchByBook: function() {
      this.query = "";
      this.byBook = true;
      this.byISBN = false;
    },
    searchByISBN: function() {
      this.query = "";
      this.byBook = false;
      this.byISBN = true;
    },
  },
  watch: {
    query: function() {
      if (this.query != false) {
        this.isClicked = true;
      } else {
        this.isClicked = false;
      }
    },
  },
};
</script>

<style scoped lang="scss">
$book: #94eae6;
$ISBN: #1ee287;

@mixin tab($color) {
  outline: none;
  border: none;
  background-color: white;
  border-bottom: 1px solid $color;
}

.search {
  #selectTab {
    width: 40%;
    margin: auto;
    margin-top: 3em;
    margin-bottom: 3em;
    .byBook {
      @include tab($book);
    }
    .bookSelected {
      background-color: $book;
      color: white;
      border-radius: 10px;
    }
    .byISBN {
      @include tab($ISBN);
    }
    .ISBNSelected {
      background-color: $ISBN;
      color: white;
      border-radius: 10px;
    }
  }
  input {
    border: none;
    outline: none;
    width: 40%;
    border-bottom: 1px solid #707070;
  }
  input.clicked {
    border-bottom: 2px solid $book;
  }
  input.ISBNIsClicked {
    border-bottom: 2px solid $ISBN;
  }
  h3 {
    margin-top: 5em;
  }
  #books {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    align-items: center;
    justify-items: center;
  }
}
</style>
