<script setup>
import { computed, watchEffect } from 'vue';
import { useListaContacs } from '../composables/useListContacts';
import DeleteButton from './DeleteBtn.vue';

const props = defineProps({
    title: {
        type: String, default: 'lista'
    },
})

const { contactList, msjEmpy, showEmpy } = useListaContacs()

watchEffect(() => {
    console.log(contactList.value)
    showEmpy('no hay resultados')
})


const totalRecompesa = computed(() => {
    return contactList.value.reduce(
        (accumulator, contact) => accumulator + contact.recompensa, 0
    )
})

const totalRecompesas = () => {
    return contactList.value.reduce(
        (accumulator, contact) => accumulator + contact.recompensa, 0
    )
}
</script>

<template>
    <div class="m-6">
        <h3 class="text-xl my-3">{{ title }} - {{ totalRecompesa }}</h3>
        <table class="table-fixed">
            <thead>
                <th>Foto</th>
                <th>Nombres</th>
                <th>numero</th>
                <th>correo</th>
                <th>acccion</th>
            </thead>
            <tbody>
                <tr v-for="contact in contactList"> 
                    <td class="p-3 border-b-2">{{ contact.id }}</td>
                    <td class="p-3 border-b-2">{{ contact.name }}</td>
                    <td class="p-3 border-b-2">{{ contact.phone }}</td>
                    <td class="p-3 border-b-2">{{ contact.email }}</td>
                    <td class="flex items-center">
                        <a href="#" class="py-2 px-4 mx-2 bg-purple-800 rounded-full">Editar</a>
                        <DeleteButton />
                    </td>
                </tr>
            </tbody>
        </table>
        <p class="text-red-800">{{ msjEmpy }}</p>
    </div>
</template>