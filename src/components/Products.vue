<template>
    <div>
        <navbar :cart="cart" :cartQty="cartQty" :cartTotal="cartTotal" @toggle-slide="toggleSlider" @delete-item="deleteItem"></navbar>
        <br>
        <h1 class="text-info font-weight-bold text-center mt-5">Boutik Kita</h1>
        <price-slider :sliderStatus="sliderStatus" :maximum.sync="maximum"></price-slider>
        <product-list :products="products" :maximum="maximum" @add-item="addItem"></product-list>
    </div>
</template>

<script>
import ProductList from "./ProductList";
import PriceSlider from "./PriceSlider";
import Navbar from "./Navbar";

export default {
    name: "products",
    props: [
        "products",
        "maximum",
        "cart",
        "cartQty",
        "cartTotal",
        "sliderStatus",
        "sliderState"
    ],
    components: {
        Navbar,
        PriceSlider,
        ProductList
    },
    methods: {
        toggleSlider: function() {
            this.$emit('toggle');
        },
        addItem: function(item) {
            this.$emit('add', item);
        },
        deleteItem: function(index) {
            this.$emit('delete', index);
        },
    }
}
</script>