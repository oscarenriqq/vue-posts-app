<script setup>
    import {onMounted, ref} from 'vue'

    import BlogPost from './components/BlogPost.vue'
    import PostPagination from './components/PostPagination.vue'
    import Loading from './components/Loading.vue'

    const loading = ref(true)

    const posts = ref([])

    onMounted(async () => {
        try {
            const res = await fetch('https://jsonplaceholder.typicode.com/posts')
            posts.value = await res.json()
        }
        catch(error) {
            console.log(error)
        } finally {
            setTimeout(() => {
                loading.value = false
            }, 1000)
        }
    })

    const postXPage = 10
    const inicio = ref(0)
    const fin = ref(postXPage)

    const favorito = ref('')

    const cambiarFavorito = (title) => {
        favorito.value = title
    }

    const nextPage = () => {
        inicio.value += postXPage
        fin.value += postXPage

    }

    const prevPage = () => {
        if (inicio.value > 0) {
            inicio.value -= postXPage
            fin.value -= postXPage
        }
    }

</script>

<template>
    <Loading v-if="loading"/>
    <div v-else class="container">
        <h1 class="text-center display-3 mb-3"> Posts App | Vue 3 </h1>
        <h2 v-if="favorito !== ''">Mis post Favoritos: {{ favorito }}</h2>
        <h2 v-else> No tienes posts favoritos.</h2>

        <PostPagination 
            class="mb-2"
            :disablePrevButton="disablePrevButton"
            :inicio="inicio"
            :fin="fin"
            @nextPage="nextPage" 
            @prevPage="prevPage" 
        />
        
        <BlogPost
            v-for="post in posts.slice(inicio, fin)"
            :key="post.id"
            :title="post.title"
            :id="post.id"
            :body="post.body"
            @cambiarFavorito="cambiarFavorito"
            class="mb-2"
        />
    </div>
</template>