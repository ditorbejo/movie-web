<script setup>
import rottenTomatoes from '../assets/rotten.png'
import metacritic from '../assets/metacrit.png'
import imdb from '../assets/imdb.png'
// const film = {
//   Title: 'Batman Forever',
//   Year: '1995',
//   Rated: 'PG-13',
//   Released: '16 Jun 1995',
//   Runtime: '121 min',
//   Genre: 'Action, Adventure',
//   Director: 'Joel Schumacher',
//   Writer: 'Bob Kane, Lee Batchler, Janet Scott Batchler',
//   Actors: 'Val Kilmer, Tommy Lee Jones, Jim Carrey',
//   Plot: 'Batman must battle former district attorney Harvey Dent, who is now Two-Face and Edward Nygma, The Riddler with help from an amorous psychologist and a young circus acrobat who becomes his sidekick, Robin.',
//   Language: 'English',
//   Country: 'United States, United Kingdom',
//   Awards: 'Nominated for 3 Oscars. 10 wins & 26 nominations total',
//   Poster:
//     'https://m.media-amazon.com/images/M/MV5BNDdjYmFiYWEtYzBhZS00YTZkLWFlODgtY2I5MDE0NzZmMDljXkEyXkFqcGdeQXVyMTMxODk2OTU@._V1_SX300.jpg',
//   Ratings: [
//     {
//       Source: 'Internet Movie Database',
//       Value: '5.4/10'
//     },
//     {
//       Source: 'Rotten Tomatoes',
//       Value: '41%'
//     },
//     {
//       Source: 'Metacritic',
//       Value: '51/100'
//     }
//   ],
//   Metascore: '51',
//   imdbRating: '5.4',
//   imdbVotes: '267,641',
//   imdbID: 'tt0112462',
//   Type: 'movie',
//   DVD: 'N/A',
//   BoxOffice: '$184,069,126',
//   Production: 'N/A',
//   Website: 'N/A',
//   Response: 'True'
// }

defineProps(['title', 'year', 'ratings', 'poster', 'director', 'writer', 'actors', 'duration'])
</script>

<template>
  <div class="h-full bg-[#8D493A] p-4">
    <div class="bg-white w-full p-2">
      <div class="flex items-center justify-center">
        <img :src="poster" class="w-full lg:w-[400px] lg:h-[400px]" alt="" />
      </div>

      <div class="flex flex-col gap-2">
        <div>
          <p class="text-2xl font-bold">
            {{ title }}
          </p>
          <p class="text-2xl font-bold">
            {{ year }}
          </p>
        </div>
        <div class="flex flex-col gap-1">
          <p class="uppercase">Ratings</p>
          <div class="flex flex-col gap-2">
            <div v-for="(item, index) in ratings" :key="index">
              <div class="grid grid-cols-2 gap-1">
                <div class="flex flex-row justify-center">
                  <img
                    v-if="item.Source === 'Internet Movie Database'"
                    :src="imdb"
                    class="h-10"
                    alt=""
                  />
                  <img
                    v-else-if="item.Source === 'Rotten Tomatoes'"
                    :src="rottenTomatoes"
                    class="h-10"
                    alt=""
                  />
                  <img v-else :src="metacritic" class="h-10" alt="" />
                </div>
                <div class="flex-row gap-2">
                  <p class="font-semibold">{{ item.Source }}</p>
                  <p>{{ item.Value }}</p>
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="flex flex-col gap-2">
          <p class="font-bold">Director: {{ director }}</p>
          <p class="font-semibold">Writer:</p>
          <p>
            {{ writer }}
          </p>
          <p class="font-semibold">Actors:</p>
          <p>
            {{ actors }}
          </p>

          <p>
            Duration: <span class="font-semibold">{{ duration }}</span>
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
