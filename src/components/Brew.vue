<template>
  <div class="container">
    <div class="row">
      <div class="col-12">
        <h1 class="text-center text-info">Breweries List</h1>
        <div class="input-group mb-3">
          <div class="input-group-prepend">
            <label class="input-group-text" for="exampleFormControlSelect1">Select State</label>
          </div>
          <select class="form-control" id="exampleFormControlSelect1" v-model="selectState">
            <option>Alabama</option>
            <option>Arkansas</option>
            <option>Arizona</option>
          </select>
        </div>
      </div>
    </div>

    <div class="row">
      <div class="col-6">
        <BrewList
          :brews="brews"
          @mouse-over-brew="mouseOverBrew"
          @mouse-left-brew="mouseLeftBrew"
        />
      </div>
      <div class="col-6">
        <BrewMap :brews="brews" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import BrewList from './BrewList.vue'
import BrewMap from './BrewMap.vue'
export default {
  name: 'Brew',
  components: {
    BrewList,
    BrewMap
  },
  data () {
    return {
      brewsRaw: [],
      normalIcon: [25, 25],
      largeIcon: [60, 60],
      selectState: 'Arizona'
    }
  },
  computed: {
    brews () {
      return this.brewsRaw.filter(r => r.state === this.selectState)
    }
  },
  mounted () {
    axios.get('https://api.openbrewerydb.org/breweries')
      .then(res => {
        this.brewsRaw = res.data.map(r => {
          r.iconSize = this.normalIcon
          return r
        })
      })
  },
  methods: {
    mouseOverBrew (id) {
      this.brewsRaw.find(element => element.id === id).iconSize = this.largeIcon
    },
    mouseLeftBrew (id) {
      this.brewsRaw.find(element => element.id === id).iconSize = this.normalIcon
    }
  }
}
</script>
