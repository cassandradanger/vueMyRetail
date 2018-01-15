<template>
    <div id="quantity-counter">
        <div class="counter">
            <h4>quantity:</h4>
            <div class="countBtn">
                <img src="../assets/minus-circle.svg"/> 
                <h3>1</h3> 
                <img src="../assets/plus-circle.svg"/>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: 'quantity-counter',
}
</script>

<style lang="scss" scoped>
    .counter{
        border: 1px solid black;
        width: 240px;
        height: 40px;
        padding: 0 5px;
    }
    .countBtn{
        float: right;
    }
    img{
        height: 40px;
        width: 40px;
        display: inline-block;
    }
    h3{
        display: inline-block;
        transform: translateY(-15px);
    }
    h4{
        display: inline-block;
        transform: translateY(-10px);
        font-weight: 100;
    }
</style>
