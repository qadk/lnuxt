<template>
    <div>
        <h1> {{post.title}} </h1>
        <p> {{post.description}} </p>

        <nuxt-link :to="{name: 'posts-id-edit', params: {id: post.id}}">Edit This Post</nuxt-link>
        <br>
        <a href="#" @click="destroy">Delete This Post</a>
        <br>
        <nuxt-link :to="{name: 'posts'}">Posts List</nuxt-link>
    </div>
</template>

<script>
    import axios from '~/plugins/axios'

    export default {
        async asyncData({params}) {
            let {data} = await axios.get(`/posts/${params.id}`)

            return {post: data}
        },
        methods: {
            destroy() {
                axios.delete(`/posts/${this.post.id}`)
                    .then(() => this.$router.replace({ path: '/posts' }))
                    .catch(function(res) {
                        alert(res)
                    })
            }
        }
    }
</script>