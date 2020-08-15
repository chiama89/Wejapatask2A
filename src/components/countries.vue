<template>
  <div class="container">
    <h1>{{ title }}</h1>
    <div>
      <label for="country">Select a Country: </label>
            <select id="country" @change='selectedCountry($event)' v-model="details.country">
               <option :value="country.name" v-for="country in countries" :key="country.id">{{ country.name }}</option>
            </select>
        <br><br>
     <label for="state">Select a State: </label>
            <select id="state" @change='selectedState($event)' v-model="details.state">
              <option :value="state.name" v-for="state in states" :key="state.id">{{ state.name }}</option>
            </select>
          <span v-if="noState">Please make a selection</span>
        <br><br>
    <label for="city">Select a City: </label>
            <select id="city" v-model="details.city">
              <option :value="city.name" v-for="city in cities" :key="city.id">{{ city.name }}</option>
            </select>
            <span v-if="noCity">Please make a selection</span>
    </div>
    <div class="details">
      <h4>County: <span v-if="details.country"> {{ details.country }}</span> </h4>
      <h4>State: <span v-if="details.state"> {{ details.state }} </span> </h4>
      <h4>City: <span v-if="details.city"> {{ details.city }} </span> </h4>
    </div>
  </div>
</template>

<script>
export default {
  name: 'countries',
  props: {
    msg: String
  },
  data() {
    return {
      title: 'Wejapa Countries',
      countries: [],
      states: [],
      cities: [],
      details: {
        country: '',
        state: '',
        city: ''
      },
      noState: false,
      noCity: false
    }
  },
  created() {
    fetch("https://raw.githubusercontent.com/dr5hn/countries-states-cities-database/master/countries%2Bstates%2Bcities.json", {
      method: "GET"
    })
      .then(response => {
        return response.json();
      })
      .then(jsonData => {
        this.countries = jsonData;
      });
  },
  methods: {
    selectedCountry(a) {
      const countryValue = a.target.value
      const country = this.countries.findIndex(a => a.name === countryValue)
      const state = this.countries[country]['states'];
      if(state.length == " "){
        this.noState = true
      }else{
      this.states = state
      }
    },
    selectedState(a) {
      const stateValue = a.target.value
      const state = this.states.findIndex(a => a.name === stateValue)
      const city = this.states[state]['cities'];
      if(city.length == " "){
        this.noCity = true
      }else{
        this.cities = city
      }
    },
  }
}
</script>

