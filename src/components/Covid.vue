<template>
  <div>
<ul>
    <input type="text" v-model="textSearch" />
    <button @click="getitem()">search</button>
</ul>
    <div class="row-ul">
    <div class="ul-2"></div>
    <div class="ul-8 center">
    <b-card-group columns>
      <b-card id="CV">
        <img :src="flag" alt="" />
        todayCases: {{ todayCases }} <br />
        todayDeaths: {{ todayDeaths }} <br />
        todayRecovered: {{ todayRecovered }} <br />
        death : {{ death }} <br />
        active :{{ active }} <br />
        activePerOneMillion:{{ activePerOneMillion }} <br />
        cases:{{ cases }}<br />
        continent: {{ continent }}<br />
        country: {{ country }}<br />
      </b-card>
    </b-card-group>
    </div>
    <div class="ul-2"></div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      textSearch: null,
      death: "",
      active: "",
      todayCases: "",
      todayDeaths: "",
      todayRecovered: "",
      updated: "",
      continent: "",
      country: "",
      flag: "",
    };
  },
  methods: {
    getitem() {
      axios
        .get("https://corona.lmao.ninja/v2/countries/" + this.textSearch)
        .then((res) => {
          this.death = res.data.deaths;
          this.active = res.data.active;
          this.activePerOneMillion = res.data.activePerOneMillion;
          this.todayCases = res.data.todayCases;
          this.todayDeaths = res.data.todayDeaths;
          this.todayRecovered = res.data.todayRecovered;
          this.cases = res.data.cases;
          this.continent = res.data.continent;
          this.country = res.data.country;

          this.flag = res.data.countryInfo.flag;
          console.log(this.flag);
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },
};
</script>
<style>
#CV {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #ffffff;
  background-color: rgb(77, 76, 73);
  position: center;
}
</style>>
