<template>
    <section class="py-12 scroll-mt-20 bg-gray-50" id="products">
        <main class="container mx-auto px-4">
            <header class="flex justify-between items-center mb-8">
                <h2 class="md:text-3xl text-2xl font-bold text-amber-900">Feature Products</h2>
                <nav class="flex space-x-4" aria-label="Product carousel controls">
                    <button @click="prevSlide" class="p-2 rounded-full bg-white shadow-md hover:bg-pink-100
                    text-pink-600 transition-colors" aria-label="Previous slide">
                        <Icon icon="line-md:arrow-small-left" width="24" height="24" />
                    </button>
                    <button @click="nextSlide" class="p-2 rounded-full bg-white shadow-md hover:bg-pink-100
                    text-pink-600 transition-colors" aria-label="Previous slide">
                        <Icon icon="line-md:arrow-small-right" width="24" height="24" />
                    </button>
                </nav>
            </header>
            <section class="relative overflow-hidden">
                <ul class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
                    <li v-for="product in visibleProducts" :key="product.id" class="bg-white rounded-lg shadow-md overflow-hidden transition-all duration-300
                    hover:scale-105">
                        <article>
                            <figure class="relative">
                                <img :src="product.image" :alt="product.name" class="w-full h-64 object-cover" />
                                <figcaption v-if="product.discount > 0"
                                    class="absolute top-3 right-3 bg-red-500 text-white text-xs font-bold px-2 py-1 rounded-full">
                                    -{{ product.discount }} %
                                </figcaption>
                                <button class="absolute top-3 left-3 p-2 bg-white rounded-full shadow-md hover:bg-pink-100
                            text-gray-700" aria-label="Add to wishlist">
                                    <Icon icon="line-md:heart" width="18" height="18" />
                                </button>
                            </figure>
                            <section class="p-4">
                                <div class="flex items-center mb-2">
                                    <Icon v-for="i in 5" :key="i" icon="line-md:star-alt-filled" width="16" height="16"
                                        :class="i <= Math.floor(product.rating) ? 'text-yellow-400' : 'text-gray-300'" />
                                    <span class="text-sm text-gray-500 ml-1">({{ product.rating }})</span>
                                </div>
                                <h3 class="text-lg font-semibold text-gray-800 mb-1">{{ product.name }}</h3>

                                <footer class="flex items-center justify-between">
                                    <div>
                                        <span class="text-lg font-bold text-pink-600">
                                            ${{ (product.price * (1 - product.discount / 100)).toFixed(2) }}
                                        </span>
                                        <span v-if="product.discount > 0"
                                            class="text-sm text-gray-500 line-through ml-2">
                                            ${{ product.price.toFixed(2) }}
                                        </span>
                                    </div>
                                    <button
                                        class="p-2 bg-pink-950 rounded-full text-white hover:bg-pink-700 transition-colors"
                                        aria-label="Add to cart">
                                        <Icon icon="icon-park-solid:shopping" width="18" height="18" />
                                    </button>
                                </footer>
                            </section>
                            <nav class="flex justify-center mt-6 space-x-2" aria-label="Carousel pagination">
                                <button v-for="index in totalSlides" :key="index" @click="currentSlide = index - 1"
                                    :class="['w-3 h-3 rounded-full', currentSlide === index - 1 ? 'bg-pink-950' : 'bg-gray-400']" />
                            </nav>
                        </article>
                    </li>
                </ul>

            </section>

        </main>

    </section>
</template>

<script setup>
import { ref, computed, onMounted, onBeforeUnmount } from 'vue';
import product from '../assets/téléchargement-removebg-preview.png';
import product1 from '../assets/images (1).jpeg';
import product2 from '../assets/images (2).jpeg';
import product3 from '../assets/images (3).jpeg';
import product4 from '../assets/images (4).jpeg';
import product5 from '../assets/images.jpeg';
import product6 from '../assets/téléchargement (1).jpeg';
import product7 from '../assets/téléchargement (2).jpeg'
const currentSlide = ref(0);
const productsPerPage = ref(4);
const products = [
    { id: 1, name: 'Floral', price: 99.99, rating: 4.5, image: product4, discount: 20 },
    { id: 2, name: 'Oriental', price: 199.99, rating: 4.5, image: product1, discount: 20 },
    { id: 3, name: 'Woody', price: 79.99, rating: 4.5, image: product2, discount: 20 },
    { id: 4, name: 'Optimus', price: 99.99, rating: 4.5, image: product6, discount: 20 },
    { id: 5, name: 'Floral', price: 99.99, rating: 4.5, image: product, discount: 20 },
    { id: 6, name: 'Floral', price: 99.99, rating: 4.5, image: product5, discount: 20 },
    { id: 7, name: 'Floral', price: 99.99, rating: 4.5, image: product3, discount: 20 },
    { id: 8, name: 'Floral', price: 99.99, rating: 4.5, image: product7, discount: 20 }
]
const totalSlides = computed(() => Math.ceil(products.length / productsPerPage.value));
const visibleProducts = computed(() => {
    const start = currentSlide.value * productsPerPage.value;
    return products.slice(start, start + productsPerPage.value)
})
const nextSlide = () => {
    currentSlide.value = currentSlide.value === totalSlides.value - 1 ? 0 : currentSlide.value + 1;
}
const prevSlide = () => {
    currentSlide.value = currentSlide.value === totalSlides.value - 1 ? 0 : currentSlide.value - 1;
}
const handleSlide = () => {
    if (window.innerWidth < 640) {
        productsPerPage.value = 1;
    } else if (window.innerWidth < 768) {
        productsPerPage.value = 2;
    } else if (window.innerWidth < 1024) {
        productsPerPage.value = 3;
    } else {
        productsPerPage.value = 4;
    }
}

onMounted(() => {
    handleSlide();
    window.addEventListener('resize', handleSlide)
})
onBeforeUnmount(() => {
    window.removeEventListener('resize', handleSlide)
})
</script>