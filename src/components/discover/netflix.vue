<template>
  <div class="gunun-populer-dizile">
    <div class="text-span">
      <span> Populaires </span>
    </div>

    <swiper
      :slides-per-view="7"
      :space-between="50"
      @swiper="onSwiper"
      @slideChange="onSlideChange"
      :mousewheel-control="false"
      :performance-mode="false"
      :pagination-visible="true"
      :pagination-clickable="false"
      navigation
      class="item ms-5"
    >
      <swiper-slide v-for="seriesList in seriesList" :key="seriesList.id">
        <div class="ms-2 me-2 movie_card item">
          <img
            :src="'http://image.tmdb.org/t/p/w500/' + seriesList.poster_path"
            class="card-img-top"
            alt="..."
          />
          <div class="film_info" v-if="isAuthenticated">
            <div class="list-icon-left">
              <a
                ><i class="fas fa-play" style="background: white; color: black">
                </i
              ></a>

              <a @click="addFavorite(seriesList)"
                ><i class="fas fa-plus toolTip">
                  <span class="toolTiptext-sm tool-span-sm">
                    Ajouter a ma liste
                  </span>
                </i></a
              >
              <i class="fas fa-chevron-down toolTip">
                <span class="toolTiptext-sm tool-span-sm">
                  Détails
                </span>
              </i>
            </div>
          </div>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>
<script>
// Import Swiper Vue.js components
import { Swiper, SwiperSlide } from "swiper/vue";
import SwiperCore, { Navigation, Pagination, Scrollbar, A11y } from "swiper";

// Import Swiper styles
import "swiper/components/navigation/navigation.scss";
import "swiper/swiper.scss";
import axios from "axios";
import { mapGetters } from 'vuex';

SwiperCore.use([Navigation, Pagination, Scrollbar, A11y]);
export default {
  components: {
    Swiper,
    SwiperSlide,
    Navigation,
  },
  data() {
    return {
      seriesList: [],
    };
  },
  methods: {
    addFavorite(seriesList) {
      axios
        .post("http://localhost:3000/favorites", {
          ...seriesList,
          isFavorite: true,
        })
        .then((response) => {
          console.log(response);
        })
        .catch((err) => console.log(err));
    },
    onSwiper(swiper) {
      console.log(swiper);
    },
    onSlideChange() {
      console.log("slide change");
    },
  },
  created() {
    axios
      .get(
        "https://api.themoviedb.org/3/trending/tv/day?api_key=b8da754884cd3ae20d385db99b95ff93"
      )
      .then((response) => {
        console.log("seriesList", response);
        this.seriesList = response.data.results;
      });
  },
  computed: {
    ...mapGetters({
      isAuthenticated: "users/isAuthenticated",
    }),
  },
};
</script>