<template>
  <div class="page_content">
    <PostsList :posts="posts" :token="token"/>
  </div>
    <Pagination :totalPages="10" :perPage="10" :currentPage="page" @pagechanged="onPageChange"/>
</template>

<script>
import axios from "axios";
import PostsList from "@/components/PostsList.vue";
import Pagination from "@/components/Pagination.vue";

export default {
  components: {
    PostsList,
    Pagination
  },
  data() {
    return {
      posts: [],
      page: 1,
      limit: 10,
      totalPages: 1,
      token: 'Y4sgKXp1AMME7JlXh5Gy7XUW9NRTL9FSmztjhQ0mcsU'
    };
  }, methods: {
    onPageChange(page) {
      console.log(page)
      this.page = page;
      this.fetchData()
    },
    async fetchData() {
      try {
        const response = await axios.get(`https://api.unsplash.com/photos/?client_id=${this.token}`, {
          params: {
            page: this.page,
            per_page: this.limit
          }
        });
        this.totalPages = Math.ceil(response.headers['x-total'] / this.limit)
        this.posts = response.data;
        console.log(this.posts)
      } catch (error) { alert("Ошибка") }
    },
  },
  mounted(){
      this.fetchData();
    }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

*,
*::before,
*::after {
    box-sizing: border-box;
}

ul,
ol {
    padding: 0;
}

body,
h1,
h2,
h3,
h4,
p,
ul,
ol,
li,
figure,
figcaption,
blockquote,
dl,
dd {
    margin: 0;
}

h1,
h2,
h3,
h4 {
    font-size: inherit;
}

ul,
ol {
    list-style: none;
}

a {
    text-decoration: none;
    color: inherit;
}

img {
    display: block;
}
button {
  cursor: pointer;
}
input,
button,
textarea,
select {
    font: inherit;
    outline: none;
    border: none;
}

body {
    font-family: 'Roboto', sans-serif;
    font-style: normal;
    font-size: 16;
    font-weight: 400;
    min-width: 320px;
    background-color: #FFFFFF;
    min-width: 280px;
}

.page_content {
  padding-bottom: 60px;
}

@media (min-width:480px) {
  .page_content {
      padding: 0 20px;
  }
}

@media (min-width:768px) {
  .page_content{
    display: grid;
    grid-template-columns: 1fr 1fr;
    column-gap: 20px;
    padding: 0 54px;
  }
}

@media (min-width:1000px) {
  .page_content{
    padding: 0 170px;
  }
}

</style>
