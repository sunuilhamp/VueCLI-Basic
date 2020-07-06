<template>
    <nav class="navbar navbar-light fixed-top">
        <div class="navbar-text ml-auto d-flex">
            <button class="btn btn-sm btn-outline-success" v-on:click="$emit('toggle-slide')">
                <font-awesome-icon icon="dollar-sign"></font-awesome-icon>
            </button>
            <div class="ml-2">
                <button class="btn btn-success btn-sm dropdown-toggle" id="dropdownCart" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                    <span class="badge badge-pill badge-success">{{ cartQty }}</span>
                    <font-awesome-icon icon="shopping-cart"></font-awesome-icon>
                    <price :value="Number(cartTotal)"></price>
                </button>
                <div class="dropdown-menu dropdown-menu-right" aria-labelledby="dropdownCart" v-if="cart.length > 0">
                    <div>
                        <div v-for="(item, index) in cart" :key="index">
                            <div class="dropdown-item-text text-nowrap text-left">
                                <span class="badge badge-pill badge-warning align-text-top mr-1">
                                    {{ item.qty }}
                                </span>
                                {{ item.product.name }}
                                
                                <b class="float-right"> 
                                    &nbsp;
                                    {{ item.product.price * item.qty | currencyFormat }}
                                    &nbsp;
                                    <a href="#" class="badge badge-danger text-white float-right" @click.stop="$emit('delete-item', index)">-</a>
                                </b>
                            </div>
                        </div>
                    </div>
                    <router-link class="btn btn-sm btn-outline-info text-dar float-right mr-2" to="/checkout">Checkout</router-link>
                </div>
            </div>
            
        </div>
    </nav>
</template>

<script>
import {FontAwesomeIcon} from "@fortawesome/vue-fontawesome";
import Price from "./Price";

export default {
    name: "navbar",
    components: {
        FontAwesomeIcon,
        Price
    },
    props: ["cart", "cartQty", "cartTotal"],
    filters: {
        currencyFormat: function (value) {
            return '$' + Number.parseFloat(value).toFixed(2)
        }
    },
}
</script>