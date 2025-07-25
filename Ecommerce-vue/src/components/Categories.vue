<template>
    <section id="categories" class="py-16 scroll-mt-20 bg-white">
        <div class="container mx-auto px-4">
            <!-- Section Header -->
            <div class="text-center mb-12">
                <h2 class="text-3xl font-bold text-amber-950 mb-3">Explore Our Fragrance Collections</h2>
                <p class="text-lg text-gray-800 max-w-2xl mx-auto">
                    Discover scents that match your personality
                </p>
            </div>
            
            <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6">
                <div v-for="(category, index) in categories"
                     :key="index"
                     class="relative group overflow-hidden rounded-lg shadow-md hover:shadow-lg transition-shadow duration-300">
                    <div class="h-64 overflow-hidden">
                        <img :src="category.image" 
                             :alt="category.alt"
                             class="w-full h-full object-cover group-hover:scale-105 transition-transform duration-500">
                    </div>
                    
                    <div class="absolute inset-0 bg-gradient-to-t from-black/60 via-transparent to-transparent">
                        <div class="absolute bottom-0 left-0 p-6">
                            <h3 class="text-xl font-semibold text-white">{{ category.title }}</h3>
                            <p class="text-gray-200 mt-1">{{ category.description }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref } from 'vue';
import product from '../assets/téléchargement-removebg-preview.png';
import product1 from '../assets/images (1).jpeg';
import product2 from '../assets/images (2).jpeg';
import product3 from '../assets/images (3).jpeg';
import product4 from '../assets/images (4).jpeg';
import product5 from '../assets/images.jpeg';
import product6 from '../assets/téléchargement (1).jpeg';
import product7 from '../assets/téléchargement (2).jpeg';

const categories = ref([
    { image: product1, title: "Men's Collection", description: "Bold & masculine scents", alt: "Men's Collection" },
    { image: product, title: "Women's Collection", description: "Elegant & feminine scents", alt: "Women's Collection" },
    { image: product2, title: "Woody Collection", description: "Warm & sophisticated scents", alt: "Woody Collection" },
    { image: product3, title: "Fresh Collection", description: "Clean & energizing scents", alt: "Fresh Collection" },
    { image: product4, title: "Oriental Collection", description: "Exotic & mysterious scents", alt: "Oriental Collection" },
    { image: product5, title: "Citrus Collection", description: "Bright & uplifting scents", alt: "Citrus Collection" }
]);
</script>