<template>
    <main class="app" >
        <h1 class="title">Cat posts!</h1>

        <div v-if="isLoading">
            Loading...
        </div>

        <div v-else>
            <div v-if="errorMessage">
                {{errorMessage}}
            </div>

            <div v-else class="list">
                <app-post-form @post="addPost"></app-post-form>
                <app-post v-for="post in posts" :key="post.id" :post="post"></app-post>
            </div>
        </div>
    </main>
</template>

<script>
    import Post from './components/Post';
    import PostForm from './components/PostForm';

    export default {
        name: 'app',
        components: {
            'app-post': Post,
            'app-post-form': PostForm
        },
        data() {
            return {
                posts: [],
                errorMessage: null,
                isLoading: true
            }
        },
        mounted() {
            fetch('https://jsonplaceholder.typicode.com/posts')
                .then((response) => response.json())
                .then((posts) => {
                    this.posts = posts.slice(0, 10);
                    this.isLoading = false;
                })
                .catch(() => {
                    this.errorMessage = 'Failed to load posts';
                    this.isLoading = false;
                })
        },
        methods: {
            addPost(event) {
                event.id = this.posts.length + 1;
                this.posts.unshift(event);
            }
        }
    }
</script>

<style scoped>
    .app {
        margin: auto;
        width: 800px;
    }

    .list {
        border: 1px lightblue solid;
        border-radius: 15px;
        padding: 5px;
    }

    .title {
        background: darkorange;
        opacity: 0.8;
        padding: 5px;
        margin-bottom: 10px;
        border-radius: 5px;
        text-align: center;
        color: darkblue;
    }
</style>
