<script lang="ts" setup>
    import type { Products } from '~/types/products';
    const props = defineProps({
        product: {
            type: Object,
            default: {},
        }
    });

    const { baseStorageUrl } = useAppConfig();
</script>

<template>
    <section class="bg-white shadow-xl rounded-xl overflow-hidden">
        <div :class="`w-full h-[200px] p-5 bg-gray-300`">
            <img :src="baseStorageUrl + props.product.image" class="w-full h-full object-contain"/>
        </div>
        <div class="px-5 pb-5 pt-9 relative">
            <NuxtLink :to="`/product/${props.product.name}`" ><h3 class="text-lg font-bold mb-4 text-limit limit-2">{{ props.product.name }}</h3></NuxtLink>
            <div class="flex justify-between items-center">
                <span class="text-sm font-normal">{{ props.product.storage }}</span>
                <span class="text-sm font-normal">${{ props.product.price }}</span>
            </div>
            <div :class="`cursor-pointer absolute -top-5 right-7 w-[50px] h-[50px] shadow-xl rounded-full flex justify-center items-center hover:bg-blue-600 hover:text-white transition duration-300 ${props.product.isCart ? 'bg-blue-600 text-white' : 'bg-white'}`">
                <i class="ri-shopping-cart-2-line"></i>
            </div>
        </div>
    </section>
</template>