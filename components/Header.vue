
import { NuxtLink } from '#build/components';
<template>
    <header class="w-full border-b border-slate-200 py-6">
        <div class="container">
            <div class="flex justify-between items-center">
                <div>
                    <NuxtLink to="/" class="text-xl font-bold">Solution Phone</NuxtLink>
                </div>
                <nav class="flex items-center gap-6">
                    <NuxtLink to="/" class="text-base">Home</NuxtLink>
                    <NuxtLink to="/product" class="text-base">Products</NuxtLink>
                    <NuxtLink to="/cart" class="text-base">Cart</NuxtLink>
                    <div class="flex justify-end gap-6">
                        <NuxtLink to="/logout" class="bg-red-500 text-white flex justify-center items-center px-3 py-2 rounded-lg">Logout</NuxtLink>
                    </div>
                </nav>
            </div>
        </div>
    </header>
</template>