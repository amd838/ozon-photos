<template>
  <div class="photo">
    <div class="photo__title">
      <span>
        ID
      </span>
      <span>
        IMG
      </span>
      <span>
        IMG TITLE
      </span>
      <span>
        ALBUM TITLE
      </span>
    </div>
    <VirtualList
      :style="listStyle"
      :data-component="itemComponent"
      :data-sources="photos"
      data-key="id"/>
  </div>
</template>

<script>
import PhotoListItem from "@/components/PhotoListItem.vue";
import VirtualList from "vue-virtual-scroll-list/src";

export default {
  name: "PhotoList",
  components: {VirtualList},
  props: {
    photos: {
      type: Array,
      required: true
    }
  },
  computed: {
    itemComponent() {
      return PhotoListItem;
    },
    listStyle() {
      return {
        height: '80vh',
        width: '100%',
        overflow: 'scroll',
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.photo {
  padding: 15px;
  &__title {
    display: grid;
    grid-template-columns: 10% 25% 25% 25%;
    margin-bottom: 15px;
  }
}
</style>
