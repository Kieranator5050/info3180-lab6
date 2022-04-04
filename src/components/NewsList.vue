<script>
export default {
    data() {
      return {
          articles : [],
          searchTerm : ''
      };        
    },

    methods: {
        searchNews() {
            let self = this;
            fetch('https://newsapi.org/v2/everything?q='+
            self.searchTerm + '&language=en', {
                headers: {
                'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,
                }
            })
                .then(function(response) {
                    return response.json();
                })
                .then(function(data) {
                    console.log(data);
                    self.articles = data.articles;
                });
        }
    },

    created() {
        
        let self = this;
        
        fetch('https://newsapi.org/v2/top-headlines?country=us', {
            headers: {
                Authorization : `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
            }
        })
            .then(function(response) {
                return response.json();
            })
            .then(function(data) {
                console.log(data);
                self.articles = data.articles;
            });
        }
};
</script>

<template>

<form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
    <div class="input-group mx-sm-3 mb-2">
        <label class="visually-hidden" for="search">Search</label>
        <input type="search" name="search" v-model="searchTerm"
        id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter search term here" />
        <button class="btn btn-primary mb-2">Search</button>
    </div>
    <p>You are searching for {{ searchTerm }}</p>
</form>


<div class="cardDisplay">
  <div v-for="article in articles" class="card cardBackground" style="width: 18rem;">
    <img :src="article.urlToImage" class="card-img-top"/>
    <div class="card-body">
      <h5 class="card-title">{{ article.title }}</h5>
      <p class="card-text">{{ article.description }}</p>
    </div>
  </div>
</div>

</template>

<style>
/* Add any component specific styles here */
.card-img-top {
    width: 100%;
    height: 15vw;
    object-fit: cover;
}

.cardDisplay{
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
}

.card{
    margin-top: 3%;
    flex: 0 1 calc(50%-1em);
}
</style>