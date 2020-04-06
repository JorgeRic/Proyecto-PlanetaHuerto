<template>
  <div class="container mx-auto">
    <h1
      class="text-green-600 my-4 text-2xl md:text-3xl lg:text-4xl text-left font-bold ml-3"
    >
      Valoraciones del producto
    </h1>
    <h3 class="text-left text-2xl pl-3 ml3 pb-5">
      Aquí puedes consultar las últimas valoraciones de los usuarios que han
      hecho sobre este producto
    </h3>

    <div class="md:w-1/2 px-3">
      <label
        for="comment"
        class="uppercase text-black text-base font-bold mb-2"
      >
        Busqueda por comentario de nuestros usuarios
      </label>
      <input
        id="comment"
        v-model="comment"
        :disabled="disabled1"
        type="text"
        class="w-full bg-gray-200
      text-black border border-gray-200 rounded py-3 px-4 mb-3"
        placeholder="Comentario usuario"
      />
    </div>
    <div class="md:w-1/2 px-3">
      <label for="author" class="uppercase text-black text-base font-bold mb-2">
        Busqueda por usuario
      </label>
      <input
        id="author"
        v-model="author"
        :disabled="disabled2"
        type="text"
        class="w-full bg-gray-200
      text-black border border-gray-200 rounded py-3 px-4 mb-3"
        placeholder="Comentario usuario"
      />
    </div>

    <div class="flex flex-wrap w-full">
      <Card
        name="star"
        v-for="review in search"
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
      reviews: db.reviews,
      comment: "",
      author: "",
      disabled1: false,
      disabled2: false
    };
  },
  methods: {},
  filters: {},
  computed: {
    search() {
      return this.reviews.filter(review => {
        if (this.comment === "" && this.author === "") return review;
        else {
          if (this.comment !== "" && this.author === "") {
            this.disabled2 = true;
            return review.comment
              .toLowerCase()
              .includes(this.comment.toLowerCase());
          } else if (this.comment === "" && this.author !== "") {
            this.disabled1 = true;
            return review.author
              .toLowerCase()
              .includes(this.author.toLowerCase());
          }
        }
      });
    }
  },
  created() {}
};
</script>
