<template>
    <main class="container-fluid px-0 d-flex justify-content-center align-items-center">
        <div v-for="(post, index) in posts" :key="index" class="card mt-2 mx-2">
            <!-- <img src="..." class="card-img-top" alt="..."> -->
            <div class="card-body">
                <h3 class="card-title">{{post.title}}</h3>
                <p class="card-text">Slug: {{post.slug}}</p>
                <p class="card-text">Description: {{truncContent(post.description, 75)}}</p>
                <p class="card-text">
                    Category: 
                    <ul>
                        <li>{{post.category?post.category.name:'-'}}</li>
                    </ul>
                </p>
                
            </div>
        </div>
    </main>
</template>
  
<script>
    export default {
        name: 'MyMain',

        data(){
            return{
                posts: []
            }
        },

        mounted(){
            this.getPost();
        },

        methods:{
            getPost(){
                axios.get('/api/posts')
                    .then((response) =>{
                        this.posts = response.data.results.data;
                    }).catch((err) =>{
                        console.log(err);
                    });
            },
            truncContent(text, textLength){
                if(text.length < textLength){
                    return text;
                }else{
                    return text.substring(0, textLength) + '...';
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    .card{
        width: 300px;
    }
</style>