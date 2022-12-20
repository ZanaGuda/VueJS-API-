<template>
  <article class="single-article">
    <div class="container">
      <div class="single-article__image">
        <img :src="'https://image.tmdb.org/t/p/w500/' + articleImage" alt="">
      </div>
      <div class="single-article__content content">
        <div >{{ articleContent }} </div>
      </div>
    </div>
  </article>
<!-- <CardItem v-for="news in similarMovies.results" :key="news.id" 
:cardTitle="news.name" 
:cardContent="news.overview"
:cardImage="news.poster_path"
:cardDate="news.first_air_date" 
:cardId="news.id">
</CardItem> -->

</template>

<script>
// import CardItem from '@/components/CardItem.vue';

export default {
    name: "SingleNews", 
    // components: { CardItem },
    data() {
        return {
            articleContent: "",
            articleImage: "",
            // similarMovies:[]
        };
    },
 
    methods: {
        fetchSingleNews(newsID) {
            fetch("https://api.themoviedb.org/3/movie/" + newsID + "?api_key=c246ec55d79f150e771a55ba99fa6c78")
                .then(response => response.json())
                .then(data => {
                console.log(data);
                this.articleContent = data.title;
                this.articleImage = data.poster_path;
            });
        },
        // fetchSimilarMovies(newsID) {
        //     fetch("https://api.themoviedb.org/3/movie/" + newsID + "/similar?api_key=c246ec55d79f150e771a55ba99fa6c78&language=en-US&page=1")
        //         .then(response => response.json())
        //         .then(data => {
        //         this.similarMovies = data
        //     });
        // },
        mounted() {
          this.fetchSingleNews(this.$route.params.id);
          // this.fetchSimilarMovies(this.$route.params.id)
        }
    },
    
}
</script>

<style>
.single-article {
  padding-top: 60px;
  padding-bottom: 60px;
  text-align: left;
}
</style>