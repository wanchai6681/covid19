<template>
  <div>
      <input type="text" v-model="textSearch"/> 
      <button @click="searchData()">search</button>
     <!-- {{playlist}} -->
    <div v-for="list in playlist" :key="list.trackId">
        <b-card-group columns>
          <b-card
            v-for = "list in playlist"
            :key="list.trackId"
            :title="list.trackName"
            :img-src="list.artworkUrl60"
            :img-alt="list.name"
            img-top
            tag="article"
            style="max-width: 20rem;"
            class="mb-2"
            >
                <b-card-text>
                    {{list.trackId}} : {{list.artistName}}
                    <audio controls>
                        <source :src="list.previewUrl" type="audio/mpeg" />

                        
                    </audio>
                </b-card-text>
            </b-card>
        </b-card-group>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
    data(){
        return{
            playlist : null,
            textSearch:"",
        }
    },
    methods :{
        searchData(){
            console.log(this.textSearch)
            axios.get('https://itunes.apple.com/search?term='+this.textSearch+'&limit=100')
            .then( (response) => {
                    this.playlist = response.data.results
                }     
            )
                .catch( (err)=> {
                        console.log(err)
                    }
                )
        }
    }
}
</script>
<style>
</style>