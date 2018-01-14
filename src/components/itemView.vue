<template>
  <div id="itemView">
    <div class="leftSide">
        <h1 class="itemTitle">{{itemData.CatalogEntryView[0].title}}</h1>
        <photo-slider :itemData="itemData"></photo-slider>
        <div class="overallReviews">
            <div class="starRating">*****</div>
            <div class="viewReviews"> view all {{this.itemData.CatalogEntryView[0].CustomerReview[0].Reviews.length}} reviews </div>
        </div>
        <div class="reviews">
            <div class="pro">
                <h3 class="reviewTitle">Pro</h3>
                <h5 class="reviewDescription">most helpful 4-5 star review</h5>
                <h4>{{this.itemData.CatalogEntryView[0].CustomerReview[0].Pro[0].title}}</h4>
                <h5>{{this.itemData.CatalogEntryView[0].CustomerReview[0].Pro[0].review}}</h5>
            
            </div>
            <div class="con">
                <h3 class="reviewTitle">Con</h3>
                <h5 class="reviewDescription">most helpful 1-2 star review</h5>
                <h4>{{this.itemData.CatalogEntryView[0].CustomerReview[0].Con[0].title}}</h4>
                <h5>{{this.itemData.CatalogEntryView[0].CustomerReview[0].Con[0].review}}</h5>

            </div>
        </div>
    </div>
    <div class="rightSide">
         <h2 class="price">{{itemData.CatalogEntryView[0].Offers[0].OfferPrice[0].formattedPriceValue}} <span class="priceQualifier">{{itemData.CatalogEntryView[0].Offers[0].OfferPrice[0].priceQualifier}}</span></h2>
        <div class="promotions" v-for="promotion in itemData.CatalogEntryView[0].Promotions">
            <h3 v-for="description in promotion.Description">{{description.shortDescription}}</h3>
        </div>
        <div class="quantityCounter">{QUANTITY COUNTER GOES HERE}</div>
        <div class="buttons">
            <button class="pickUp">PICK UP IN STORE</button>
            <button class="addToCart">ADD TO CART</button>
        </div>
        <h3 class="returns">returns | <span class="returnPolicy">This item must be returned within 30 days of the ship date. See {return policy} for details. Prices, promotions, styles and availibility may vary by store and online.</span></h3>
        <div class="buttons">
            <button>ADD TO REGISTRY</button>
            <button>ADD TO LIST</button>
            <button>SHARE</button>
        </div>
        <h4 v-for="feature in features">{{feature}}</h4>
    </div>
  </div>
</template>

<script>
import PhotoSlider from './photoSlider.vue';

    export default {
        name: 'itemView',
        props: ['itemData'],
        components:{
            PhotoSlider,
        },
        data(){
            return {
                features: [],
                highestRated: [],
                lowestRated: [],
            }
        },
        created(){
            this.populateFeatures();
            this.populateRatings();
        },
        methods:{
            populateFeatures(){
                let items = this.itemData.CatalogEntryView[0].ItemDescription;
                items.map((item) => {
                    item.features.map((feature) => {
                        this.features.push(feature);
                    })
                });
            },
        }
    }
</script>

<style lang="scss" scoped>
    #itemView{
        margin: 200px 100px 100px 225px;
    }
    .leftSide{
        width: 49%;
        float: left;
        border: 1px solid black;
    }
    .rightSide{
        width: 49%;
        float: right;
        border: 1px solid black;
    }
</style>
