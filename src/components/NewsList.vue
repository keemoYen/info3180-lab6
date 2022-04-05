<template>
    <form @submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
        <div class="input-group mx-sm-3 mb-2">
            <label class="visually-hidden" for="search">Search</label>
            <input type ="search" name="search" v-model ="searchTerm"
            id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter search term here"/>

            <button class="btn btn-primary mb-2">Search</button>
        </div>
        <p>You are searching for {{ searchTerm }}</p>
    </form>
    
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
           articles: [],
           searchTerm: ''
       }
    },
    methods:{
        searchNews(){
            let self = this;

            fetch('https://newsapi.org/v2/everything?q='+self.searchTerm+'&language=en',{
                headers:{
                    'Authorization': 'Bearer 2796a2c49d354b9e9dde6e5e7bdf6f44'
                }
            })
            .then(function(response) {
                return response.json();
            })
            .then(function(data){
                console.log(data);
                self.articles = data.articles;
            });
        }
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

<style>
    .news__list{
        display: grid;
        grid-template-columns: auto auto auto;
    }

    ul{
        list-style-type: none;
    }
</style>