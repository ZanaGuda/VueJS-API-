<template>
<div class="card">
    <router-link :to="'/single-movie/'+ cardId">
        <div class="card-image">
            <figure class="image is-4by3">
                <img :src="'https://image.tmdb.org/t/p/w500/'+ cardImage" :alt="cardTitle">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
                <div class="media-content">
                    <p class="title is-4">{{cardTitle}}</p>
                </div>
            </div>

            <div class="content">
                <div >{{ cardContent }}</div>
                <time datetime="2016-1-1">{{cardDate}}</time>
            </div>
        </div>
    </router-link>
</div>
</template>

<script>
export default {
    name: 'CardItem',
    props: {
        cardTitle: String,
        cardContent: String,
        cardImage: String,
        cardDate: String,
        cardId: Number
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style scoped>
.image.is-4by3 {
  padding-top: 150%;
}
</style>
