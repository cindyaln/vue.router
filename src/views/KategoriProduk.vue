<template>
    <h1>Kategori {{ KategoriProduk.nama }}</h1>
    <div class="flex-container">
     <div v-for="produk in state" :key="produk.id" class="card">
      <router-link class="container" :to="{ name: 'Detail', params: { id_produk: produk.id }}">
      <h4>{{ produk.nama }}</h4>
      </router-link>
    </div>
    </div>
  </template>
  <script>
  import { onMounted, reactive } from 'vue'
  import { produk } from '@/assets/produk'
  import { kategori } from '@/assets/kategori'
  
  export default{
    props: [
        "id_kategori"
      ],
    setup (props, context)
  {
    const KategoriProduk= kategori["kategori"].find(function(item){
          return item.id == props.id_kategori;
        });
    const state = reactive(produk["produk"]);
  
  onMounted(() => {
        context.emit("id-menu", 5);
    });
    return{
      state,
      KategoriProduk
    }
   }
  }
  </script >
  
  <style scoped>
.flex-container {
    display: flex;
}
.card {
    box-shadow: 0 4px 8px 0 rgba(0,0, 0, 0.2);
    transition: 0.3s;
    margin: 10px;
    min-width: 200px;
    cursor: pointer;
}
.card:hover {
    box-shadow: 0 8px 16px 0 rgba(0,0, 0, 0.2);
}
.container {
    padding: 2px 16px;
}
img {
    width: 200px;
    height: 200px;
}
</style>