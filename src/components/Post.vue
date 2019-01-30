<template>
    <div class="post">
        <img :src="image"
             width="100px"
             height="100px"
             alt="Cat">
        <div class="post-data">
            <h4 class="title">{{post.title}}</h4>
            <p class="body">{{post.body}}</p>
        </div>
    </div>
</template>

<script>
    export default {
        name: "Post",
        props: {
            post: {
                type: Object,
                required: true,
                validator:  (post) => post.title && post.id && post.body,
            }
        },
        computed: {
            image() {
                const id = this.post.id;
                const isEven = id % 2 === 0;
                if (isEven) {
                    return `https://cataas.com/cat/gif?id=${id}`
                } else {
                    return `https://cataas.com/cat?id=${id}`
                }
            }
        }
    }
</script>

<style scoped>
    .post {
        padding: 5px;
        margin: 10px 5px;
        border-radius: 30px;
        display: flex;
        justify-content: center;
        align-items: center;
        background: linear-gradient(to right, #F9D423AA, #FF4E50AA)
    }

    img {
        width: 100px;
        height: 100px;
        border-radius: 50%;
        padding: 5px;
        flex-shrink: 0;
        border: 2px darkblue solid;
        margin-right: 20px;
    }

    .post-data {
        flex: 1;
    }

    .title {
        font-size: 1.2rem;
    }
</style>
