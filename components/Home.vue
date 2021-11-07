<template>
  <div class="lg:container mx-auto p-2 text-center">
    <img
      src="../assets/bg.jpg"
      class="bg fixed top-0 left-0 w-full h-full"
      alt=""
    />
    <h1 class="text-white text-4xl p-3 mb-4">Election news.</h1>
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mx-auto">
    <div class="card bg-white rounded-md hover:shadow-2xl" v-for="(item, index) in searchResults.response.docs" :key="index">
        <h2 class="text-black p-4 text-lg font-bold">{{ item.abstract}}</h2>
        <p class="card__description text-justify p-3 pb-0">
          {{ item.lead_paragraph }}
        </p>
        <a class="text-blue-400 pb-3" :href="item.web_url" target="_blank">
          Read more...
        </a>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
        base_url: "https://api.nytimes.com/svc/search/v2/articlesearch.json?q=election&api-key=",
        api_key: "W3TG8BoFxypq0N0gqGWJAkSbMYwb7Jbj",
        searchResults: {
            response: {
                docs: [
                ]
            }
        },
    };
},
    created() {
        axios
        .get(this.base_url + this.api_key)
        .then((response) => {
            this.searchResults = response.data;
            console.log(this.searchResults);
        })
        .catch((e) => {
            console.log(e);
        });
    },
};
</script>

<style>
.bg {
  z-index: -1;
}
.card{
    transition: 0.3s ease-in-out;
}
.card:hover{
    transform: translateY(-10px);
}
</style>