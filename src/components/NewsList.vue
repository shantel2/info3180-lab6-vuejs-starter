<template>
 <div class='news'>
    <section v-for="article in articles" class="card">

        <img class="news-img" v-bind:src="article.urlToImage" :alt="article.title" />
        <div class="card-body">
            <h5>{{ article.title }}</h5>
            <p class= "description"> {{ article.description }}</p>
        </div>
    
    </section>
 </div>
</template>

<script>
export default {
 data() {
    return {
        articles: []
    }
 },
 created() {
    let self = this;
    fetch('https://newsapi.org/v2/top-headlines?country=us',
    {
        headers: {
            'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`
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
}
</script>


<style>

ul{
    list-style-type: none;
}

.news{
    display: grid;
    grid-template-columns: repeat(3,1fr);
    grid-column-gap: 30px;
}

.news-img{
    width: 25.7rem;
    height: 20rem;
}


.card{
    margin-bottom: 15px;
}
</style>