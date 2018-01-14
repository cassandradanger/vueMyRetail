<template>
    <div id="photo-slider">
        <img :src="mainImage" class="mainImage"/>
        <div class="gallery">
            <button class="back" @click="goBack"><</button>
            <img :src="image" v-for="image in thumbnailArray" :class="mainImage === image ? 'selectedThumbnail' : 'thumbnailImage'" @click="selectImage(image)"></img>
            <button class="forward" @click="goForward">></button>
        </div>
    </div>
</template>

<script>

export default {
  name: 'photo-slider',
  props: ['itemData'],
  data(){
    return {
        thumbnailArray: [],
        mainImage: this.itemData.CatalogEntryView[0].Images[0].PrimaryImage[0].image,
        currentIndex: 0,
    }
  },
  created(){
      this.itemData.CatalogEntryView[0].Images[0].AlternateImages.map((image) => {
          this.thumbnailArray.push(image.image);
          console.log(this.thumbnailArray);
      })
  },
  methods: {
    goBack(){
        if(this.currentIndex > 0){
            this.currentIndex =  this.currentIndex - 1;
        } else {
            this.currentIndex = this.thumbnailArray.length;
        }
        console.log(this.currentIndex);
        this.mainImage = this.thumbnailArray[this.currentIndex];
        console.log(this.mainImage);
    },
    goForward(){
        if(this.currentIndex < this.thumbnailArray.length){
            this.currentIndex =  this.currentIndex + 1;
        } else {
            this.currentIndex = 0;
        }
        console.log(this.currentIndex);
        this.mainImage = this.thumbnailArray[this.currentIndex];
        console.log(this.mainImage);
    },
    selectImage(image){
        this.mainImage = image;
        console.log(image);
    },
  }
}
</script>

<style lang="scss">
.mainImage{
    display: block;
    margin: 0 auto;
    border: 1px solid black;
}
.gallery{
    margin: 20px auto;
    border: 1px solid black;
    display: inline-block;
    text-align: center;
}
.back .forward{
    display: inline-block;
}
.thumbnailImage{
    height: 75px;
    width: 75px;
    display: inline-block;
    margin: 10px;
}

.selectedThumbnail{
    height: 75px;
    width: 75px;
    display: inline-block;
    margin: 10px;
    border: 1px solid lightgrey;
    border-radius: 4px;
}
</style>
