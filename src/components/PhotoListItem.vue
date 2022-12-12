<template>
  <div class="photo-list__item">
    <span>
      {{source.id}}
    </span>
    <img :src="source.thumbnailUrl" />
    <span>
      {{source.title}}
    </span>
    <span>
      {{source.albumTitle}}
    </span>
  </div>
</template>

<script>
export default {
  name: "PhotoListItem",
  props: {
    source: {
      type: Object,
      required: true
    }
  }
}
</script>

<style lang="scss" scoped>
.photo-list__item {
  display: grid;
  grid-template-columns: 10% 25% 25% 25%;
}
</style>
