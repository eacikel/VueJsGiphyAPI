<template>
    <div class="search">
        <input placeholder="Aranacak kelime giriniz..." type="text" v-model="query" @keyup.enter="handleSearch"><!-- v-model il inputtaki text ne zaman değişirse query değişkeni o zaman değişir ve o değeri alır -->
        <button @click="handleSearch">Ara</button>
    </div>
</template>

<script>
export default { 
    data() { // vue, componentlerinde data her zaman bir function olup functionda bir obje dönmesini ister. Bu component'in reusability (tekrar kullanılabilirlik) arttırır.
        return {
            query: ''
        }
    },
    methods: {
        handleSearch() {
            this.$emit('SearchRequested', this.query); // vue, data'nın içindeki her key2i alıp instance'a kendisi koyar (query'i koydu)
        }
    }
}
</script>>

<style>
    .search input {
        padding: 10px 20px;
        border: 1px solid #CCC;
        border-radius: 5px;
        width: 300px;
    }

    .search button {
        padding: 5px 15px;
        border: 1px solid #CCC;
        background-color: coral;
        color: white;
        font-size: 20px;
        border-radius: 5px;
    }
</style>