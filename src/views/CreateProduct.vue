<template>
    <main class="container py-[50px]">

        <div class="head flex justify-between items-center">
            <h2 class="text-3xl text-gray-700">Create product</h2>
            <button class="btn py-2 px-7 bg-blue-600 text-white rounded hover:opacity-80"
                @click="$router.push({ name: 'home' })">
                <i class="fas fa-home mr-2"></i>
                <span>Go Home</span>
            </button>

        </div>

        <form class="form w-full max-w-[400px] mx-auto p-5 rounded bg-white shadow" @submit.prevent="createProduct">
            <h3 class="text-xl mb-2">New Product</h3>
            <!--  -->
            <div class="form-controll mb-1">
                <label for="name" class="inline-block w-full text-sm text-gray-400">Product name</label>
                <input type="text" id="name" class="input" v-model.trim="product.name">
                <p class="error-message text-xs text-red-400" v-if="errors.name">
                    {{ errors.name }}
                </p>
            </div>
            <!--  -->
            <div class="form-controll mb-1">
                <label for="description" class="inline-block w-full text-sm text-gray-400">Product description</label>
                <input type="text" id="description" class="input" v-model.trim="product.description">
                <p class="error-message text-xs text-red-400" v-if="errors.description">
                    {{ errors.description }}
                </p>
            </div>
            <!--  -->
            <div class="form-controll mb-1">
                <label for="price" class="inline-block w-full text-sm text-gray-400">Product price</label>
                <input type="text" id="price" class="input" v-model.number="product.price">
                <p class="error-message text-xs text-red-400" v-if="errors.price">
                    {{ errors.price }}
                </p>
            </div>
            <!--  -->
            <div class="form-controll mb-1">
                <label for="image" class="inline-block w-full text-sm text-gray-400">Product image</label>
                <input type="text" id="image" class="input" v-model.trim="product.image">
                <p class="error-message text-xs text-red-400" v-if="errors.image">
                    {{ errors.image }}
                </p>
            </div>

            <div class="action flex justify-end">
                <button class="btn px-5 py-2 text-white bg-blue-500 rounded">
                    <i class="fas fa-plus mr-2"></i>
                    <span>Create</span>
                </button>
            </div>

        </form>

    </main>
</template>



<script>

export default {
    data() {
        return {
            errors: {
                name: '',
                description: '',
                price: '',
                image: ''
            },
            product: {
                name: '',
                description: '',
                price: '',
                image: ''
            }
        }
    },
    computed: {
        isValid() {
            if(this.errors.name && this.errors.description && this.errors.price && this.errors.image){
                return true
            } else {
                return false
            }
        }
    },

    watch: {
        product: {
            handler(newValue) {
                if (newValue.name.length < 5) {
                    this.errors.name = 'Minimum length is 5'
                } else if (newValue.name.length > 20) {
                    this.errors.name = 'At least 20 characters'
                } else {
                    this.errors.name = ''
                }


                if (newValue.description.length < 5) {
                    this.errors.description = 'Minimum length is 5'
                } else if (newValue.description.length > 50) {
                    this.errors.description = 'At least 50 characters'
                } else {
                    this.errors.description = ''
                }


                if (newValue.price.length < 1) {
                    this.errors.price = 'Minimum length is 1'
                } else if (typeof newValue.price !== 'number') {
                    this.errors.price = 'Enter only numbers!'
                } else {
                    this.errors.price = ''
                }

                const httpRegex = /^https?:\/\/(?:www\.)?[-a-zA-Z0-9@:%._\+~#=]{1,256}\.[a-zA-Z0-9()]{1,6}\b(?:[-a-zA-Z0-9()@:%_\+.~#?&\/=]*)$/;

                if (newValue.image.length < 1) {
                    this.errors.image = 'Minimum length is 1'
                } else if (httpRegex.test(!newValue.image)) {
                    this.errors.image = 'Enter correct image url!'
                } else {
                    this.errors.image = ''
                }
            },
            deep: true
        }

    },
    methods: {
        createProduct() {
            console.log(this.product)
        }
    }

}


</script>

<style> .input {
     @apply inline-block w-full rounded p-2 shadow outline-blue-400;

 }
</style>