<template>
    <div class="container-fuild">
        
            <div v-for="article in articles" :key="article" style="display: inline-block; margin: 10px;" >
                <div class="card" style="width:300px; height: 480px;">
                    <img class="card-img-top" style="width: 300px; height: 200px;" :src="`${article.urlToImage}`" alt="Card image">
                    
                        <h5 class="card-title">{{ article.title }}</h5>

                        <div id="dsc" v-html="`${article.description}`"></div>

                    
               </div>
            </div>
            
            <!--
                <img style="width: 300px; height: 300px; margin: 10px;" alt="image" src="{{ url_for('get_image', filename=file.img) }}" /></li>
            -->
        
    </div>
</template>

<script>
    export default {
        data() {
            return {
                articles: []
            };
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