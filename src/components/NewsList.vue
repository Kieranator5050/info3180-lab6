<script>
export default {
    data() {
      return {
          articles : []
      };        
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