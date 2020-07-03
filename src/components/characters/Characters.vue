<template>
    <section>
        <input class="border my-5 w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" type="text" placeholder="Filter by character name" v-model="searchKey"/>
        <div class="grid sm:grid-cols-1 md:grid-cols-2 grid-flow-row gap-4 content-center">
            <CharacterItem v-for="character in filterCharacters" :key="character.char_id" v-bind:character="character"></CharacterItem>
        </div>
        <div class="flex my-5 justify-center" v-if="characters.length && !searchKey">
            <button class="bg-white-500 hover:bg-white-800 text-black font-bold py-2 px-4 border" v-on:click="loadMore()">Load More </button>
        </div>
        <Spinner v-if="loading"/>
    </section>
</template>

<script>
import axios from 'axios'
import CharacterItem from '@/components/characters/CharacterItem'
import Spinner from '@/components/ui/Spinner'
export default {
  name: 'Characters',
  data () {
    return {
      characters: [],
      limit: 10,
      offset: 0,
      searchKey: '',
      loading: false
    }
  },
  components: {
    CharacterItem,
    Spinner
  },
  mounted () {
    this.getCharacters()
  },
  computed: {
    filterCharacters () {
      if (this.characters.length) {
        return this.characters.filter(character => {
          return character.name
            .toLowerCase()
            .includes(this.searchKey.toLowerCase())
        })
      } else {
        return []
      }
    }
  },
  methods: {
    async getCharacters () {
      this.loading = true
      try {
        const params = {
          limit: this.limit,
          offset: this.offset
        }
        const response = await axios.get('https://www.breakingbadapi.com/api/characters', { params })
        this.loading = false
        this.characters.push(...response.data)
      } catch (error) {
        this.loading = false
        console.log(error)
      }
    },
    loadMore () {
      this.offset += 10
      this.getCharacters()
    }
  }
}
</script>

<style>

</style>
