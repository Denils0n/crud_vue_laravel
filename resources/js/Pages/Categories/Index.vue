<script setup>
import AuthenticatedLayout from '@/Layouts/AuthenticatedLayout.vue';
import { Head, useForm } from '@inertiajs/vue3';

defineProps({
    categories: {
        type: Object,
        required: true
    }
})

const createForm = useForm({
    nomezinho: ''
})

const add = () => {
    createForm.post(route('cat.store'), {
        onFinish: () => {

        }
    })
}

const remove = (cat) => {
    const id = prompt('esse id mesmo, mano?', cat.id)
    useForm({}).delete(
        route('cat.destroy', id)
    )
}
</script>

<template>
    <Head title="Categoties" />

    <AuthenticatedLayout>
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 dark:text-gray-200 leading-tight">Categories</h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white dark:bg-gray-800 overflow-hidden shadow-sm sm:rounded-lg">
                    <div class="p-6 text-gray-900 dark:text-gray-100">
                        Minhas categorias bonitinhas
                        <div v-for="category in categories" class="my-4 border-b">
                            {{ category }}
                            <a href="#" @click.prevent="remove(category)">Delete</a>
                        </div>

                        <form @submit.prevent="add">
                            <input type="text" v-model="createForm.nomezinho">
                            <button>Save</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </AuthenticatedLayout>
</template>
