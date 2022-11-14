<script setup>
import { ref, onMounted } from 'vue';
import BlogPost from './components/BlogPost.vue';
import PaginatePos from './components/PaginatePost.vue'
import LoadingSpinner from './components/LoadingSpinner.vue'


const fav = ref('');
const selectFav = (id) => {
	fav.value = id;
};

const posts = ref([])
const postXpage = 5;
const inicio = ref(0);
const fin = ref(postXpage);
const loading = ref(true);
const next = () => {
	inicio.value += postXpage;
	fin.value += postXpage
}

const prev = () => {
	inicio.value += - postXpage;
	fin.value += - postXpage
}

//Opcion 1, cuando se monte el apartado del componente
onMounted(async () => {
	try {
		const res = await fetch('https://jsonplaceholder.typicode.com/posts')
		posts.value = await res.json()
	} catch (error) {
		console.log(error);
	} finally {
		setTimeout(() => {
			loading.value = false
		}, 2000);
	}
})

//Opcion 2, cuando recien empiece a cargar la pantalla
// fetch('https://jsonplaceholder.typicode.com/posts')
// 	.then(res => res.json())
// 	.then(data => posts.value = data)
// 	.catch(e => console.error(e))
// 	.finally(() => {
// 		setTimeout(() => {
// 			loading.value = false
// 		}, 2000)
// 	});

</script>

<template>
	<LoadingSpinner v-if="loading" />
	<div class="container" v-else>
		<h1>App</h1>
		<br>
		<h2>Mis Post favoritos : {{ fav }}</h2>

		<PaginatePos class="mb-2" @next="next" @prev="prev" :inicio="inicio" :fin="fin" :maxPosts="posts.length" />

		<BlogPost v-for="post in posts.slice(inicio, fin)" :key="post.id" :title="post.title" :id="post.id"
			:body="post.body" @selectFav="selectFav" class="mb-2" />

	</div>
</template>
