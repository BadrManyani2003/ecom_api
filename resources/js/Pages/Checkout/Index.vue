<template>
    <div>
        <Menu></Menu>
        <div class="container mx-auto p-6">
            <!-- Page Title -->
            <h1 class="text-3xl font-bold text-gray-800 mb-6">Checkout</h1>
            <div>
                <div v-if="cart.length === 0" class="text-gray-500">Your cart is empty.</div>
                <div v-else>
                    <table class="table-auto w-full border-collapse border border-gray-300">
                        <thead>
                            <tr class="bg-gray-100">
                                <th class="border border-gray-300 px-4 py-2">Img</th>
                                <th class="border border-gray-300 px-4 py-2">Name</th>
                                <th class="border border-gray-300 px-4 py-2">Price</th>
                                <th class="border border-gray-300 px-4 py-2">Quantity</th>
                                <th class="border border-gray-300 px-4 py-2">Subtotal</th>
                                <th class="border border-gray-300 px-4 py-2">Manage</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="item in cart" :key="item.id" class="text-center">
                                <td class="border border-gray-300 px-4 py-2"> <img :src="item.img_url"
                                        alt="Product Image" class="w-16 h-16 object-cover rounded" /></td>
                                <td class="border border-gray-300 px-4 py-2">{{ item.name }}</td>
                                <td class="border border-gray-300 px-4 py-2">{{ item.price }}</td>
                                <td class="border border-gray-300 px-4 py-2">{{ item.quantity }}</td>
                                <td class="border border-gray-300 px-4 py-2">{{ (item.price *
                                    item.quantity).toFixed(2) }}</td>
                                <td class="border border-gray-300 px-4 py-2"> <button @click="removeFromCart(item.id)"
                                        class="ml-4 text-red-500">X</button>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            <!-- Checkout Form Section -->
            <div v-if="cart.length > 0" class="mt-8">
                <h2 class="text-xl font-semibold mb-4">Checkout Form</h2>
                <form @submit.prevent="handleSubmit">
                    <!-- Name -->
                    <div class="mb-4">
                        <label for="name" class="block text-sm font-medium mb-2">Name</label>
                        <input type="text" v-model="form.name" id="name" class="w-full p-2 border rounded"
                            placeholder="Enter your name" required />
                    </div>

                    <!-- Phone -->
                    <div class="mb-4">
                        <label for="phone" class="block text-sm font-medium mb-2">Phone</label>
                        <input type="text" v-model="form.phone" id="phone" class="w-full p-2 border rounded"
                            placeholder="Enter your phone number" required />
                    </div>

                    <!-- Address -->
                    <div class="mb-4">
                        <label for="address" class="block text-sm font-medium mb-2">Address</label>
                        <textarea v-model="form.address" id="address" class="w-full p-2 border rounded"
                            placeholder="Enter your address" required></textarea>
                    </div>

                    <!-- Email -->
                    <div class="mb-4">
                        <label for="email" class="block text-sm font-medium mb-2">Email</label>
                        <input type="email" v-model="form.email" id="email" class="w-full p-2 border rounded"
                            placeholder="Enter your email" required />
                    </div>

                    <!-- Submit Button -->
                    <div class="flex justify-end">
                        <button type="submit" class="bg-teal-500 text-white px-4 py-2 rounded">Place Order</button>
                    </div>
                </form>
            </div>

            <!-- If Cart is Empty -->
            <div v-else class="text-gray-500">Please add items to your cart before proceeding.
            </div>
        </div>

    </div>
</template>

<script>
import axios from 'axios';
import Menu from '../Includes/Menu.vue';
export default {
    components: {
        Menu,
        axios
    },
    data() {
        return {
            cart: [], // To hold the cart data
            form: {
                name: '',
                phone: '',
                address: '',
                email: '',
            },
        };
    },
    mounted() {
        // Fetch the cart data from localStorage
        const savedCart = localStorage.getItem('cart');
        if (savedCart) {
            this.cart = JSON.parse(savedCart);
        }


    },

    removeFromCart(productId) {
        this.cart = this.cart.filter(item => item.id !== productId);
    },
}
</script>

<style lang="scss" scoped></style>