<template>
    <div>
        <h1>Checkout</h1>
        <table class="table table-hover" v-if="cart.length">
            <caption class="text-right h3">
                <b>Total:</b>
                <price class="d-block text-success font-weight-light"
                    :value="Number(cartTotal)"></price>
            </caption>
            <thead>
                <tr>
                    <th></th>
                    <th>Item</th>
                    <th class="text-left">Image</th>
                    <th class="text-center">Qty</th>
                    <th class="text-right">Price</th>
                    <th class="text-right">Subtotal</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="(item,index) in cart" :key="item.product.id">
                    <td class="text-center">
                        <button @click="$emit('add', item.product)" class="btn btn-info">+</button>
                        <button @click="$emit('delete', index)" class="btn btn-outline-info">-</button>
                    </td>
                    <th scope="row">{{ item.product.name }}</th>
                    <td class="float-left"><img :src="item.product.image" alt="item.name" height="150"></td>
                    <th class="text-center">{{ item.qty }}</th>
                    <th class="text-right">{{ Number(item.product.price) }}</th>
                    <th class="text-right">{{ Number(item.product.price) * item.qty }}</th>
                </tr>
            </tbody>
        </table>
        <router-link class="btn btn-sm btn-outline-info text-dar" to="/">Back to Shop</router-link>
    </div>
</template>

<script>
import Price from "./Price";

export default {
    name: "checkout",
    props: [
        "cart",
        "cartTotal"
    ],
    components: {
        Price
    }    
}
</script>