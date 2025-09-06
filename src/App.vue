<script setup>
  import ListContacts from './components/ListContacts.vue';
  import SearchContacts from './components/SearchContacts.vue';
  import { getAllContacts } from './services/apiContacs';
  import { useListaContacs } from './composables/useListContacts';

  const { contactList } = useListaContacs()
  const title = 'Lista de contactos'

  const clearList = (newList) => {
    contactList.value = newList
  }

  const filterListContact = (kword) => {
    if (kword.trim() === '') {
      contactList.value = getAllContacts()
    }
    contactList.value = contactList.value.filter(
      (contact) => {
        return contact.name.toLowerCase().includes(kword.toLowerCase())
      }
    )
  }

</script>

<template>
  <div class="flex items-center flex-col p-5">
    <h1 class="text-xl m-4"> {{ title }} </h1>

    <search-contacts @filterContact="filterListContact"/>
    
    <list-contacts title="Lista de Resultados"/>

    <div>
      <button 
        class="bg-blue-500 py-1.5 px-5"
        @click="clearList()"
      >
        Limpiar
      </button>
    </div>
  </div>
</template>