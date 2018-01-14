<template>
    <div id="photo-slider">
        <div class="mainImage"><img :src="this.itemData.CatalogEntryView[0].Images[0].PrimaryImage[0].image"/></div>
        <div class="gallery">
            <button class="back"><</button>
            <div class="array"></div>
            <button class="forward">></button>
        </div>
    </div>
</template>

<script>
import itemData from '../assets/item-data.json';

export default {
  name: 'photo-slider',
  components: {
    itemData,
  },
  data(){
    return {
        itemData: itemData,
    }
  }
}
</script>

<style lang="scss">
</style>
