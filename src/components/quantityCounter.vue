<template>
    <div id="quantity-counter">
        <div class="counter">
            <h4>quantity:</h4>
            <div class="countBtn">
                <img @click="decreaseCount" src="../assets/minus-circle.png"/> 
                <h3>{{count}}</h3> 
                <img @click="increaseCount" src="../assets/plus-circle.png"/>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'quantity-counter',
    data(){
        return {
            count: 1,
        }
    },
    methods:{
        increaseCount(){
            this.count++;
        },
        decreaseCount(){
            this.count--;
        }
    },
}
</script>

<style lang="scss" scoped>
    .counter{
        border: 1px solid black;
        width: 227px;
        height: 40px;
        padding: 0 5px;
    }
    .countBtn{
        float: right;
    }
    img{
        height: 30px;
        width: 30px;
        display: inline-block;
    }
    h3{
        display: inline-block;
        transform: translateY(-15px);
        padding: 0 10px;
    }
    h4{
        display: inline-block;
        transform: translateY(-10px);
        font-weight: 100;
    }
</style>
