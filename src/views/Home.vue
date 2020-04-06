<template>
  <div class="container mx-auto">
    <h1
      class="text-green-600 my-4 text-2xl md:text-3xl lg:text-4xl text-left font-bold ml-3"
    >
      Valoraciones del producto
    </h1>
    <!-- <ul v-for="dato in datos" :key="dato.id">
      <li>{{ dato | tiempo(10) }}</li>
    </ul> -->
    <Search name="star" :reviews="reviews"> </Search>
    <h3 class="text-left text-2xl pl-3 ml3 pb-5">
      Aquí puedes consultar las últimas valoraciones de los usuarios que han
      hecho sobre este producto
    </h3>
    <div class="flex flex-wrap w-full">
      <Card
        name="star"
        v-for="review in reviews"
        :key="review.id"
        :review="review"
      >
      </Card>
    </div>
  </div>
</template>
<script>
import Card from "@/components/Card.vue";
import Search from "@/components/Search.vue";
import db from "@/assets/db.json";
export default {
  name: "home",
  components: {
    Card,
    Search
  },
  data: function() {
    return {
      nombre: "jorge",
      isLoaded: false,
      reviews: db.reviews
    };
  },
  filters: {
    // tiempo: function(value, minutos) {
    //   if (value.tiempo < minutos) return value.nombre;
    // }
  },

  created() {},
  methods: {}
};
</script>
