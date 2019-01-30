<template>
    <form @submit.prevent.stop="submit"
          @keydown.exact.enter.stop.prevent="submit">

        <input :class="{ 'my-class': myCondition }" type="text" v-model="post.title" name="title" placeholder="title">
        <div class="error-message" v-if="error.field === 'title'">{{error.message}}</div>

        <textarea rows="3" v-model="post.body" name="body" placeholder="body"></textarea>
        <div class="error-message" v-if="error.field === 'body'">{{error.message}}</div>

        <button type="submit">POST</button>
    </form>
</template>

<script>
    export default {
        name: 'PostForm',
        data() {
          return {
              post: {
                  title: '',
                  body: ''
              },
              error: {
                  field: '',
                  message: ''
              }
          }
        },
        methods: {
            checkForm() {
                const { post } = this;
                this.error = { field: '', message: '' };
                if (!post.title) {
                    this.error = {
                        field: 'title',
                        message: 'This form requires a title'
                    };
                }
                if (!post.body) {
                    this.error = {
                        field: 'body',
                        message: 'This form requires a body'
                    };
                }
            },
            submit() {
                this.checkForm();
                if(this.error.field) {
                    return;
                }
                this.$emit('post', {...this.post});
                this.post.title = '';
                this.post.body = '';
            }
        }
    }
</script>

<style scoped>
    form {
        display: flex;
        flex-direction: column;
        margin: auto;
    }

    input, textarea {
        border-radius: 15px;
        border: 1px solid lightblue;
    }


    textarea::placeholder, input::placeholder, input, textarea {
        font-size: 1rem;
        padding: 5px;
        margin: 5px;
        outline: none;
    }

    textarea {
        resize: none;
    }

    button {
        margin: 5px;
        padding: 10px;
        font-size: 1.2rem;
        background: linear-gradient(to right, #8CA6DB, #B993D6);
        max-width: 200px;
        border-radius: 15px;
        border: none;
        cursor: pointer;
        color: white;
    }

    .error-message {
        color: red;
        padding: 5px;
    }
</style>
