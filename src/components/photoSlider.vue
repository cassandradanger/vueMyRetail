<template>
    <div id="photo-slider">
        <img :src="mainImage" class="mainImage"/>
        <div class="gallery">
            <button class="back" @click="goBack"><</button>
            <!-- <img :src="image" v-for="image in thumbnailArray.slice(slice1, slice2)" :class="mainImage === image ? 'selectedThumbnail' : 'thumbnailImage'" @click="selectImage(image)"></img> -->
            <img :src="thumbnailArray[image1]" :class="mainImage === thumbnailArray[image1] ? 'selectedThumbnail' : 'thumbnailImage'" @click="selectImage(thumbnailArray[image1])"></img>
            <img :src="thumbnailArray[image2]" :class="mainImage === thumbnailArray[image2] ? 'selectedThumbnail' : 'thumbnailImage'" @click="selectImage(thumbnailArray[image2])"></img>
            <img :src="thumbnailArray[image3]" :class="mainImage === thumbnailArray[image3] ? 'selectedThumbnail' : 'thumbnailImage'" @click="selectImage(thumbnailArray[image3])"></img>
            
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
        image1: 0,
        image2: 1,
        image3: 2,
    }
  },
  created(){
      this.thumbnailArray.push(this.itemData.CatalogEntryView[0].Images[0].PrimaryImage[0].image);
      this.itemData.CatalogEntryView[0].Images[0].AlternateImages.map((image) => {
          this.thumbnailArray.push(image.image);
      })
  },
  methods: {
    goBack(){
        this.image1--;
        this.image2--;
        this.image3--;

        if(this.image1 < 0){
            this.image1 = this.thumbnailArray.length -1;
        }
        if(this.image2 < 0){
            this.image2 = this.thumbnailArray.length -1;
        }
        if(this.image3 < 0){
            this.image3 = this.thumbnailArray.length -1;
        }

        if(this.currentIndex > 0){
            this.currentIndex =  this.currentIndex - 1;
        } else {
            this.currentIndex = this.thumbnailArray.length - 1;
        }
        this.mainImage = this.thumbnailArray[this.currentIndex];
    },
    goForward(){
        this.image1++;
        this.image2++;
        this.image3++;

        if(this.image1 > this.thumbnailArray.length -1){
            this.image1 = 0;
        }
        if(this.image2 > this.thumbnailArray.length -1){
            this.image2 = 0;
        }
        if(this.image3 > this.thumbnailArray.length -1){
            this.image3 = 0;
        }

        if(this.currentIndex < this.thumbnailArray.length -1){
            this.currentIndex =  this.currentIndex + 1;
        } else {
            this.currentIndex = 0;
        }
        this.mainImage = this.thumbnailArray[this.currentIndex];
    },
    selectImage(image){
        this.mainImage = image;
        this.currentIndex = this.thumbnailArray.indexOf(image);
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
