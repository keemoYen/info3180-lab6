<template>
    <ul class="news__list">
        <li v-for="article in articles" class ="news__item">
            <div class="card" style="width: 18rem;">
                <img v-bind:src="article.urlToImage" class="card-img-top" alt="news Image">
                <div class="card-body">
                    <h5 class="card-title">{{article.title}}</h5>
                    <p class="card-text">{{article.description}}</p>
                    <a v-bind:href="article.url" class="btn btn-primary">Visit Article</a>
                </div>
            </div>
        </li>
            
    </ul>
</template>

<script>
export default {
    data() {
       return{
           articles: []
       }; 
    },
    created(){
        let self = this;

        fetch('https://newsapi.org/v2/top-headlines?country=us',
        {
            headers:{
                'Authorization':  'Bearer 2796a2c49d354b9e9dde6e5e7bdf6f44'//'Bearer $import.meta.env.VITE_NEWSAPI_TOKEN'
            }
        })
        .then(function(response){
            return response.json();
        })
        .then(function(data){
            console.log(data);
            self.articles = data.articles;
        });
    }
};
</script>