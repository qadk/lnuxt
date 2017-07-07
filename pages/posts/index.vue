<template>
    <div>
        <nuxt-link :to="{name: 'posts-create'}">Create Post</nuxt-link>
        <div v-for="post in posts">
            <nuxt-link :to="{ name: 'posts-id', params: { id: post.id }}"><h1> {{post.title}} </h1></nuxt-link>
            <p> {{post.description}} </p>
        </div>
    </div>
</template>

<script>
    import axios from '~/plugins/axios'

    export default {
        async asyncData() {
            let {data} = await axios.get(`/posts`)

            return {posts: data}
        }
    }
</script>