<template>
  <div id="itemView">
    <div class="leftSide">
        <h1 class="itemTitle">{{itemData.CatalogEntryView[0].title}}</h1>
        <photo-slider :itemData="itemData"></photo-slider>
        <div class="overallReviews">
            <div class="starRating">***** overall</div>
            <div class="viewReviews">view all {{this.itemData.CatalogEntryView[0].CustomerReview[0].Reviews.length}} reviews </div>    
        </div>
        <div class="reviews">
            <hr class="reviewLine"/>
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
        <hr class="line"/>
        <div class="promotions" v-for="promotion in itemData.CatalogEntryView[0].Promotions">
            <h3 v-for="description in promotion.Description">{{description.shortDescription}}</h3>
        </div>
        <hr class="line"/>
        <div class="quantityCounter">{QUANTITY COUNTER GOES HERE}</div>
        <div class="buttons">
            <button class="pickUp">PICK UP IN STORE</button>
            <button class="addToCart">ADD TO CART</button>
        </div>
        <h3 class="returns">returns | <span class="returnPolicy">This item must be returned within 30 days of the ship date. See <a href="#"><strong>return policy</strong></a> for details. Prices, promotions, styles and availibility may vary by store and online.</span></h3>
        <div class="buttons">
            <button class="subButton">ADD TO REGISTRY</button>
            <button class="subButton">ADD TO LIST</button>
            <button class="subButton">SHARE</button>
        </div>
        <h1 class="highlights">product highlights</h1>
        <ul v-for="feature in features">
            <li>{{feature}}</li>
        </ul>
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
        },
        methods:{
            populateFeatures(){
                let items = this.itemData.CatalogEntryView[0].ItemDescription;
                items.map((item) => {
                    item.features.map((feature) => {
                        let newFeature = feature.replace('<strong>', '')
                        newFeature = newFeature.replace('</strong>', '');
                        this.features.push(newFeature);
                    })
                });
            },
        }
    }
</script>

<style lang="scss" scoped>
    a{
        text-decoration: none;
        color: inherit;
    }
    h5{
        font-weight: 100;
        margin-top: 0;
    }
    h4{
        margin: 45px 0 5px;
    }
    #itemView{
        margin: 200px 75px 75px 225px;
    }
    .leftSide{
        width: 500px;
        display: inline-block;
    }
    .rightSide{
        width: 500px;
        display: inline-block;
        position: absolute;
        margin-left: 20px;
    }
    .itemTitle{
        font-weight: 100;
        text-align: center;
        font-size: 26px;
        width: 85%;
        margin: 20px auto;
    }
    .priceQualifier{
        font-size: 10pt;
        font-weight: 100;
        margin: 30px 0;
    }
    .line, .reviewLine{
        color: grey;
    }
    .reviewLine{
        transform: translateY(60px);
        color: black;
    }
    .promotions h3{
        color: #cb0e17;
        margin: 10px;
        font-size: 12pt;
    }
    .returns{
        font-weight: 100;
        font-size: 14pt;
    }
    .returnPolicy{
        font-weight: 100;
        font-size: 8pt;
        width: 85%;
        float: right;
    }
    .subButton{
        border-radius: 0;
        border-color: transparent;
        background-color: #eeeeee;
        color: black;
        width: 163px;
        height: 25px;
    }
    .pickUp{
        color: white;
        font-size: 16pt;
        font-weight: 100;
        width: 240px;
        height: 40px;
        background-color: black;
        border-radius: 0;
    }
    .addToCart{
        color: white;
        font-size: 16pt;
        font-weight: 100;
        width: 240px;
        height: 40px;
        background-color: #cb0e17;
        border-radius: 0;
        margin-left: 15px;
    }
    .buttons{
        margin: 30px 0;
    }
    .highlights{
        font-weight: normal;
    }
    ul{
        padding-left: 17px;
    }
    .starRating{
        font-size: 12pt;
        display: inline-block;
    }
    .viewReviews{
        font-size: 12pt;
        display: inline-block;
        float: right;
    }
    .reviews{
        padding: 0 10px 30px;
        background-color: #eeeeee;
    }
    .pro, .con{
        margin: 0;
        width: 45%;
        display: inline-block;
        vertical-align: top;
    }
    .con{
        float: right;
    }
    .reviewTitle{
        font-weight: 100;
        margin: 0;
    }
    .reviewDescription{
        margin: 0 0 5px;
        font-weight: 100;
    }
</style>
