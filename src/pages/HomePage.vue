<script setup>
import CardMovieComponent from '../components/CardMovieComponent.vue'
import DetailFilmPage from '../components/DetailFilmPage.vue'
import { ref, onMounted } from 'vue'
const apiKey = '28745c2'
const searchTerm = ref('')
const popularValue = 'ghost'
const detailFilm = ref('')
const listMovie = ref([])
const showModal = ref(false)

async function searchFilm() {
  console.log(searchTerm)
  const response = await fetch(`http://www.omdbapi.com/?s=${searchTerm.value}&apikey=${apiKey}`)
  if (!response.ok) {
    throw new Error('Network response was not ok')
  }
  const data = await response.json()
  if (data.Response === 'True') {
    console.log(data.Search)
    listMovie.value = []
    listMovie.value.push(...data.Search)
    console.log(listMovie.value)
  } else {
    console.error('Error:', data.Error)
  }
}

async function handleChangeSearch(name) {
  console.log('value', name)
  if (name.value !== null) {
    const response = await fetch(`http://www.omdbapi.com/?s=${name}&apikey=${apiKey}`)
    if (!response.ok) {
      throw new Error('Network response was not ok')
    }
    const data = await response.json()
    if (data.Response === 'True') {
      console.log(data.Search)
      listMovie.value = []
      listMovie.value.push(...data.Search)
      console.log(listMovie.value)
    } else {
      console.error('Error:', data.Error)
    }
  } else {
    listMovie.value = []
  }
}

async function getPopularFilm() {
  console.log(searchTerm)
  const response = await fetch(`http://www.omdbapi.com/?s=${popularValue}&apikey=${apiKey}`)
  if (!response.ok) {
    throw new Error('Network response was not ok')
  }
  const data = await response.json()
  if (data.Response === 'True') {
    console.log(data.Search)
    listMovie.value.push(...data.Search)
    console.log(listMovie.value)
  } else {
    console.error('Error:', data.Error)
  }
}

async function getDetailFilm(item) {
  console.log(item)
  const idFilm = item.imdbID
  console.log(console.log('ini id film', idFilm))
  const response = await fetch(`http://www.omdbapi.com/?i=${idFilm}&apikey=${apiKey}`)
  if (!response.ok) {
    throw new Error('Network response was not ok')
  }
  const data = await response.json()
  console.log(data)
  detailFilm.value = data
  console.log(detailFilm.value)
  showModal.value = true
  console.log('ini show modal', showModal.value)
}

function closeModal() {
  console.log('close modal')
  showModal.value = false
}

onMounted(async () => {
  await getPopularFilm()
})
</script>

<template>
  <div class="flex flex-col p-4 gap-4 relative">
    <div>
      <p class="text-3xl font-bold text-center bg-stone-400 rounded-2xl">Movie Pack</p>
    </div>
    <div class="">
      <p class="font-bold text-2xl">Search film</p>
      <div class="flex flex-row w-full justify-between gap-4 h-10">
        <input
          type="text"
          class="border border-black w-full rounded-2xl p-2"
          v-model="searchTerm"
          @input="handleChangeSearch(searchTerm)"
          placeholder="Ketik film disini"
        />
        <button
          class="bg-yellow-800 px-3 py-2 rounded-2xl text-white capitalize"
          @click="searchFilm()"
        >
          search
        </button>
      </div>
    </div>
    <div><p class="text-2xl font-bold">Popular 2024</p></div>
    <div class="grid grid-cols-2 lg:grid-cols-4 gap-4">
      <div v-for="(item, index) in listMovie" :key="index" @click="getDetailFilm(item)">
        <CardMovieComponent
          :title="item.Title"
          :year="item.Year"
          :ratings="item.Ratings"
          :type="item.Type"
          :poster="item.Poster"
        ></CardMovieComponent>
      </div>
    </div>
  </div>

  <div
    :class="[
      'h-screen w-full fixed right-0 overflow-y-auto top-0 bg-black p-2 z-10 md:flex md:items-center md:justify-center',
      showModal ? 'translate-x-0' : 'translate-x-full'
    ]"
  >
    <div class="flex items-center justify-center relative">
      <DetailFilmPage
        :title="detailFilm.Title"
        :year="detailFilm.Year"
        :ratings="detailFilm.Ratings"
        :poster="detailFilm.Poster"
        :director="detailFilm.Director"
        :actors="detailFilm.Actors"
        :duration="detailFilm.Runtime"
      ></DetailFilmPage>
    </div>

    <button class="p-4 bg-white h-12 w-12 absolute top-0 right-0" @click="closeModal()">X</button>
  </div>
</template>
