<script setup>
import { ref, reactive } from 'vue';
import { useListaContacs } from '../composables/useListContacts';

const emit = defineEmits(['filterContact',])

const stylesBtn = reactive({
    'background': 'blue',
    'color': 'blank'
})

const kword = ref('')
const { msjEmpy, showEmpy } = useListaContacs()

const isFocus = () => {
    stylesBtn.background = 'grey'
    stylesBtn.color = 'white'
}

const filtrarDatos = () => {
    showEmpy('Pruebe otra palabra')
    emit('filterContact', kword.value)
}
</script>

<template>
    <div class="flex items-center">
        <input type="text" class="block flex-1 border-0 bg-white py-1.5 pl-1 text-gray-900 placeholder:text-gray-400" placeholder="buscar.." @focus="isFocus" @input="filtrarDatos()" v-model="kword">

        <button class="bg-blue-500 py-1.5 px-5" :style="stylesBtn" @click="$emit('searchContacts')">Buscar</button>
    </div>
    <p class="text-red-500">{{ msjEmpy }}</p>
</template>