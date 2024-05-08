<template>
    <div v-if="post.id" class="p-4">
        <h2 class="text-xl font-bold uppercase">{{ post.title }}</h2>
        <small class="text-gray-500"> Autor:{{ post.userId }}</small>
        <p class="text-gray-700">{{ post.body }}</p>
    </div>
    <div v-else class="p-4">
        <p>Cargandoooo</p>
    </div>
</template>

<script>


export default {
    name: "PostPage",
    props: ["id"],
    data() {
        return {
            post: {}, // Se usará para almacenar el post
        };
    },
    created() {
        this.getPost();
    },
    methods: {
        getPost() {
            // axios
            //     .get(`${API_URL}/${this.id}`)
            //     .then((response) => {
            //         this.post = response.data;
            //     });
        },
    },
    watch: {
        id() {
            this.getPost();
        },
    },
};
</script>