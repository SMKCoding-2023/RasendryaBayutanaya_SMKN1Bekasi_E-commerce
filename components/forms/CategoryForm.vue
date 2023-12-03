<script lang="ts" setup>
    import { useCategoryStore } from '~/stores/category';
    import type { Category } from '~/composables/constants/category';
    // const categories = ref(Category);
    const isLoading = ref(false);
    const isShowAlert = ref(false);
    const message = ref("");
    const router = useRouter();
    const categoryStore = useCategoryStore();
    const formCreateCategory = [
        { name: "name", label: "Name", type: "text", value: "", placeholder: "Write in here", required: true },
    ];

    const createCategory = async () => {
        isLoading.value = true;
        const result: { [key: string]: any } = {};
        formCreateCategory.forEach((item: Category) => {
            if(item.name){
                result[item.name] = item.value;
            }
        });
        await categoryStore.createCategory(result);
        if (categoryStore.status){
            isShowAlert.value = true;
            message.value = categoryStore.message;
            isLoading.value = false;
            window.scrollTo({
                top: 0,
                behavior: "smooth",
            });
            setTimeout(() => {
                router.push({ path: "/category/create" });
            }, 1000);
        }
    }
</script>
<template>
    <section class="flex justify-center py-10">
        <div class="w-[500px]">
            <h1 class="text-2xl mb-7 font-medium">Create Category</h1>
            <div v-if="isShowAlert" class="p-4 mb-4 text-sm rounded-lg bg-green-100 text-green-800">{{ message }}</div>
            <form @submit.prevent="createCategory()">
                <div class="mb-6" v-for="(item, index) in formCreateCategory" :key="index">
                    <label :for="item.name" class="block mb-2 text-sm font-medium text-gray-900"> {{ item.label }} </label>
                    <input :type="item.type" :id="item.name" v-model="item.value" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5" :placeholder="item.placeholder" :required="item.required">
                </div>
                <button type="submit" class="text-white bg-primary hover:bg-primary/80 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center">
                    <span v-if="!isLoading">Submit</span>
                    <div v-else class="flex items-center gap-3">
                        <div class="w-5 h-5 rounded-full border-2 border-t-blue-500 animate-spin"></div>
                    <span>Loading</span>
            </div>
                </button>
            </form>
        </div>
    </section>
</template>