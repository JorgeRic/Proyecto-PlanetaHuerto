<template>
  <!-- <div
    class="container inline-flex flex-row col-xl-3 col-lg-3 col-md-5 col-sm-10 col-10 m-4"
  > -->

  <div class="w-full md:w-1/2 lg:w-1/3 ">
    <div class=" card">
      <div class="flex justify-start ml-2 my-4">
        <div class="inline-flex items-center text-base font-semibold">
          <div v-for="starts in 5" :key="starts">
            <svg
              class="start"
              :class="{ icon1: starts > review.rating }"
              v-show="starts"
              width="20"
              height="20"
            >
              <use v-bind="{ 'xlink:href': '/feather-sprite.svg#' + name }" />
            </svg>
          </div>
          <h6 class="ml-3 text-gray-600 mt-1">{{ review.rating }}.0</h6>
        </div>
      </div>
      <div class="text-left ml-2 mb-3 text-gray-600">
        <span>
          {{ review.author }},
          <!-- {{ dateComment() }} -->
          {{ review.date | getDate }}
        </span>
      </div>
      <div class="ml-2 mr-4 text-lg flex content-start flex-wrap">
        <h5 class="leading-relaxed text-justify text-xl">
          {{ review.comment }}
        </h5>
        <h5 class="leading-relaxed text-justify">
          <!-- {{ review.comment | firstLetterUppercase }} -->
        </h5>
      </div>
      <div class="flex ml-2 py-2">
        <button
          @click="addUser"
          :disabled="disabled"
          :class="['rounded', backgroundButton]"
        >
          <div class="flex flex-no-wrap my-2 mx-3 ">
            <svg
              class="fill-current text-black mr-2"
              :class="{ icon3: push }"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 24 24"
              width="21"
              height="21"
            >
              <path
                class="heroicon-ui"
                d="M17.62 10H20a2 2 0 0 1 2 2v8a2 2 0 0 1-2 2H8.5c-1.2 0-2.3-.72-2.74-1.79l-3.5-7-.03-.06A3 3 0 0 1 5 9h5V4c0-1.1.9-2 2-2h1.62l4 8zM16 11.24L12.38 4H12v7H5a1 1 0 0 0-.93 1.36l3.5 7.02a1 1 0 0 0 .93.62H16v-8.76zm2 .76v8h2v-8h-2z"
              />
            </svg>
            <small :class="{ icon3: push }"> Es útil</small>
          </div>
        </button>
        <div class="flex items-center content-center ml-3">
          <span class="change-users" v-if="sum <= 1"
            >{{ sum }} persona cree que es útil</span
          >
          <span class="change-users" v-else
            >{{ sum }} personas creeís que es útil</span
          >
        </div>
      </div>
      <!-- <div>
            <button
              type="button"
              @click="sumItems"
              class="btn btn-info mt-3 mb-3"
            >
              Sum Items
            </button>
            <span class="pl-1">El comentario tiene: {{ items }} items.</span>
          </div>
          <div>
            <button
              type="button"
              @click="sumLetters"
              class="btn btn-info mt-3 mb-3"
            >
              Sum Letters
            </button>
            <span class="pl-1">El comentario tiene: {{ letters }} letras</span>
          </div> -->
    </div>
  </div>
</template>
<script>
// import "bootstrap/dist/css/bootstrap.min.css";
// import moment from "moment";

export default {
  props: {
    review: Object,
    name: String
  },
  data() {
    return {
      sum: this.review.useful_count,
      disabled: false,
      backgroundButton: "bg-gray-100",
      push: false,
      items: 0,
      letters: 0
    };
  },
  methods: {
    addUser() {
      this.sum = this.review.useful_count += 1;
      this.disabled = true;
      this.backgroundButton = "bg-green-600";
      this.push = true;
    }
    // sumItems() {
    //   let totalItems = 1;
    //   for (var i = 0; i < this.review.comment.length; i++) {
    //     totalItems++;
    //   }
    //   this.items = totalItems;
    // },
    // sumLetters() {
    //   let espacios = 0;
    //   for (var i = 0; i < this.review.comment.length; i++) {
    //     let vale = this.review.comment[i] === " ";
    //     if (vale === false) {
    //       espacios = espacios + -1;
    //       this.letters = 0 + this.review.comment[i] - espacios;
    //     }
    //   }
    // }
    // dateComment() {
    //   const date = moment(this.review.date)
    //     .locale("es")
    //     .format("LL");
    //   return date;
    // }
  },
  filters: {
    // firstLetterUppercase: value => {
    //   for (var i = 0; i < value.length; i++) {
    //     let vale = value[i] === " ";
    //     // console.log(vale);
    //     if (vale === false) {
    //       console.log(value);
    //       value[i] = value[i].charAt(0).toUpperCase() + value[i].slice(1);
    //       console.log(value[i]);
    //     }
    //   }

    // let words = value.split("");
    // let newArray = [];
    // for (var i = 0; i < words.length; i++) {
    //   // console.log(words[i]);

    //   let vale = newArray[i] === " ";
    //   console.log(vale);
    //   // console.log(newArray);
    //   if (vale === false) {
    //     newArray.push(words[i]);
    //   }

    //   if (newArray.length % 2 !== 0 && vale === false) {
    //     // console.log(newArray);
    //     // console.log(newArray[i]);

    //     newArray[i] =
    //       newArray[i].charAt(0).toUpperCase() + newArray[i].slice(1);
    //   }
    // }

    // return newArray.join("");
    // },

    firstLetterUppercase: value => {
      let words = value.split("");
      let newArray = [];
      for (var i = 0; i < words.length; i++) {
        // if (words[i] !== " ") {
        newArray.push(words[i]);
        // }
        if (newArray.length % 2 !== 0 && newArray !== " ") {
          // console.log(newArray);
          // console.log(newArray[i]);
          newArray[i] =
            newArray[i].charAt(0).toUpperCase() + newArray[i].slice(1);
        }
      }

      return newArray.join("");
    },
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
  }
};
</script>

<style scoped>
.icon1 {
  fill: white;
}
.icon3 {
  fill: white;
}
</style>
