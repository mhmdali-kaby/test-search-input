<template>
  <div id="app">
    <input
        type="text"
        v-model="searchQuery"
        placeholder="Search..."
        @input="searchArticles"
    />
    <div v-if="filteredArticles.length">
      <div v-for="(article, index) in filteredArticles" :key="index" class="article">
        <span v-html="highlightText(article)"></span>
      </div>
    </div>
    <div v-else>
      <p>No results found.</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      searchQuery: "",
      articles: [
        "This is a test article.",
        "We are testing the search functionality.",
        "Vue.js is a great framework for building SPAs.",
        "Search for your favorite articles here.",
      ],
      filteredArticles: [],
    };
  },
  methods: {
    searchArticles() {
      if (this.searchQuery.trim() === "") {
        this.filteredArticles = [];
        return;
      }

      const query = this.searchQuery.toLowerCase();
      this.filteredArticles = this.articles.filter((article) =>
          article.toLowerCase().includes(query)
      );
    },
    highlightText(article) {
      const query = this.searchQuery;
      if (!query.trim()) return article;

      const regex = new RegExp(`(${query})`, "gi");
      return article.replace(regex, '<span class="highlight">$1</span>');
    },
  },
};
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  padding: 20px;
  max-width: 500px;
  margin: auto;
}
input {
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  border: 1px solid #ccc;
  border-radius: 5px;
}
.article {
  margin-bottom: 10px;
}
.highlight {
  background-color: yellow;
  font-weight: bold;
}
</style>
