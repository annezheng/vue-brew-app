<template>
  <div class="brew-list">
    <div class="card"
      v-for="(brew, index) in brews"
      :key="index"
      @mouseover="mouseOver(brew.id)"
      @mouseleave="mouseLeave(brew.id)"
    >
      <div class="card-body" >
        <h5 class="card-title">{{ brew.name }}</h5>
        <h6 class="card-subtitle mb-2 text-muted">{{ brew.city }}, {{ brew.state }}</h6>
        <p class="card-text">
          <span class="text-muted">Phone:</span> {{ brew.phone }}<br>
          <span class="text-muted">Address:</span> {{ brew.street }}
        </p>
        <a :href="brew.website_url" class="card-link text-info">Website</a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'BrewList',
  props: {
    brews: Array
  },
  methods: {
    mouseOver (id) {
      this.$emit('mouse-over-brew', id)
    },
    mouseLeave (id) {
      this.$emit('mouse-left-brew', id)
    }
  }
}
</script>

<style scoped lang="scss">
.brew-list {
  border: 1px dashed grey;
  overflow-y: scroll;
  height: 90vh;
  .card {
    &:hover {
      background-color: #92cfd9;
    }
  }
}
</style>