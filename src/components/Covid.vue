<template>
  <div>
    <input type="text" v-model="textSearch" />
    <button @click="getitem()">search</button>
  <ul/>
    <!-- {{playlist}} -->
    <div v-for="list in playlist" :key="list.trackId"></div>
    <div>
    todayCases: {{todayCases}}  <br>
    todayDeaths: {{todayDeaths}}  <br>
    todayRecovered: {{todayRecovered}}  <br>
    death : {{ death }} <br>
    active :{{ active }} <br>
    activePerOneMillion:{{activePerOneMillion}}  <br>
    cases:{{cases}}<br>
    continent: {{continent}}<br>
    country: {{country}}<br>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  data(){
    return{
      textSearch:null,
      death : '',
      active:'',
      todayCases: '',
      todayDeaths: '',
      todayRecovered: '',
      updated: '',
      continent: '',
      country: '' 
    }
  },

  methods:{
    getitem(){
      axios.get('https://corona.lmao.ninja/v2/countries/' + this.textSearch)
      .then(res => {
        this.death = res.data.deaths
        this.active = res.data.active
        this.activePerOneMillion=res.data.activePerOneMillion
        this.todayCases =res.data.todayCases
        this.todayDeaths=res.data.todayDeaths
        this.todayRecovered=res.data.todayRecovered
        this.cases=res.data.cases
        this.continent=res.data.continent
        this.country=res.data.country
        console.log(res.data)
      })
      .catch(err => {
        console.error(err); 
      })
      
  }
    
}

}
</script>