<template>
    <div>
        <input type="text" v-model="post.title">
        <input type="text" v-model="post.description">
        <button @click="summit">Summit</button>
    </div>
</template>

<script>
    import axios from '~/plugins/axios'

    export default {
        data(){
            return {
                post: {
                    title: '',
                    description: ''
                }
            }
        },

        methods: {
            summit(){
                axios.post(`/posts`, this.post)
                    .then((res) => {
                        this.$router.replace({ path: '/posts' })
                    })
                    .catch(function(res){
                        alert(res)
                    })
            }
        }
    }
</script>