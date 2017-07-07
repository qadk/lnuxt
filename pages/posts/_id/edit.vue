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
        async asyncData({params}) {
            let {data} = await axios.get(`/posts/${params.id}/edit`)

            return {post: data}
        },

        methods: {
            summit(){
                axios.put(`/posts/${this.post.id}`, this.post)
                    .then((res) => {
                        this.$router.replace({ name: 'posts-id', params:{id: this.post.id} })}
                        )
                    .catch(function(res){
                        alert(res)
                    })
            }
        }
    }
</script>