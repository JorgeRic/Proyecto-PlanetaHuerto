<template>
  <div>
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
        type="text"
        class="w-full bg-gray-200
      text-black border border-gray-200 rounded py-3 px-4 mb-3"
        placeholder="Comentario usuario"
      />
    </div>

    <div>
      <div class="" v-for="review in searchComment" :key="review.id">
        <div class="card w-full md:w-1/2">
          <h6 class="ml-3 text-gray-600 mt-1">
            Valoracion de usuarios: {{ review.rating }}.0
          </h6>
          <div class="ml-2 mr-4 text-lg flex content-start flex-wrap">
            <h5 class="leading-relaxed text-justify text-xl">
              {{ review.comment }}
            </h5>
            <div class="text-left ml-2 mb-3 text-gray-600">
              <span>
                {{ review.author }},
                {{ review.date | getDate }}
              </span>
            </div>
            <h5 class="leading-relaxed text-justify"></h5>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  props: {
    reviews: Array,
    comment: String
  },
  data() {
    return {};
  },
  filters: {
    getDate: value => {
      let months = [
        "enero",
        "febrero",
        "marzo",
        "abril",
        "mayo",
        "junio",
        "julio",
        "agosto",
        "septiembre",
        "octubre",
        "noviembre",
        "diciembre"
      ];
      let fecha = new Date(value);
      return (
        fecha.getDate() +
        " " +
        "de" +
        " " +
        months[fecha.getMonth()] +
        " " +
        "de" +
        " " +
        fecha.getFullYear()
      );
    }
  },
  computed: {
    searchComment() {
      return this.reviews.filter(review =>
        review.comment.includes(this.comment)
      );
    }
  }
};
</script>
