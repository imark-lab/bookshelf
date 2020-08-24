<template>
  <div class="book">
    <a class="imgLink" :href="link" target="_blank" rel="noopener noreferrer"
      ><img :src="img"
    /></a>
    <h4>{{ title }}</h4>
    <p class="author" v-if="authors">
      著者：<span v-for="(author, index) in authors" :key="index"
        >{{ authors.length >= 2 ? index + 1 + "." + author : author }}
      </span>
    </p>
    <p class="lang">言語：{{ lang }}</p>
    <p class="pages">ページ数：{{ page }}</p>
    <p class="type">仕様：{{ jpBook(printType) }}</p>
    <p class="date">刊行：{{ date }}</p>
    <a :href="link" class="link">Read more</a>
  </div>
</template>

<script>
export default {
  name: "ShowBooks",
  props: {
    img: String,
    title: String,
    authors: Array,
    link: String,
    lang: String,
    date: String,
    printType: String,
    page: Number,
  },
  methods: {
    jpBook: function(book) {
      if (book == "BOOK") {
        return "本";
      }
    },
  },
};
</script>

<style scoped lang="scss">
div.book {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(5, 3em);
  align-items: center;
  justify-items: center;
  border: 1px solid #94eae6;
  border-radius: 5px;
  width: 90%;
  margin-bottom: 5em;
  padding: 1em;

  .imgLink {
    grid-column: 1/2;
    grid-row: 1/5;
  }
  img {
    height: 100%;
    width: 100%;
    object-fit: scale-down;
  }
  h4 {
    grid-column: 2/4;
    grid-row: 1/3;
  }
  .author {
    grid-column: 2/3;
    grid-row: 3/4;
  }
  .lang {
    grid-column: 3/4;
    grid-row: 3/4;
  }
  .pages {
    grid-column: 2/3;
    grid-row: 4/5;
  }
  .type {
    grid-column: 3/4;
    grid-row: 4/5;
  }
  .date {
    grid-column: 1/2;
    grid-row: 5/6;
  }
  a.link {
    grid-column: 2/4;
    grid-row: 5/6;
    padding: 0.5em;
    font-weight: bold;
    border: 1px solid #94eae6;
    color: white;
    background-color: #94eae6;
    border-radius: 10px;
  }
}
</style>
