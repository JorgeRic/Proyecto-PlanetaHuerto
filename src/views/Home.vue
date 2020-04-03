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
import db from "@/assets/db.json";
export default {
  name: "home",
  components: {
    Card
  },
  data: function() {
    return {
      nombre: "jorge",
      isLoaded: false,
      reviews: db.reviews
      // datos: [
      //   { nombre: "Hacer la compra", tiempo: 12 },
      //   { nombre: "Aprender Vue.js", tiempo: 5 },
      //   { nombre: "Lavar el coche", tiempo: 22 }
      // ]
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
