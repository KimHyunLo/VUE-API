<template>
  <div>
    <HeaderCont />
    <TitleCont name1="Movie" name2="api" />
    <div className="top_movies">
      <span className="title">
        <h1>Top Movies</h1>
      </span>
      <swiper
        :slidesPerView="4"
        :space-between="-50"
        :loop="true"
        :autoplay="{
          delay: 4000,
          disableOnInteraction: false,
        }"
        :navigation="true"
        :pagination="pagination"
        :modules="modules"
      >
        <swiper-slide v-for="vid in top" :key="vid.id">
          <div className="top-item">
            <a :href="`https://www.themoviedb.org/movie/${vid.id}`">
              <img
                :src="`https://image.tmdb.org/t/p/w342${vid.poster_path}`"
                :alt="vid.title"
              />
            </a>
          </div>
        </swiper-slide>
      </swiper>
    </div>
    <div className="movie__search">
      <form @submit.prevent="SearchMovies()">
        <div className="container">
          <h2>검색하기</h2>
          <input
            type="search"
            id="search"
            placeholder="검색하세요."
            v-model="search"
          />
          <button type="submit">검색</button>
        </div>
      </form>
    </div>
    <div className="movie__cont">
      <div className="container">
        <div className="movie__list">
          <ul>
            <li v-for="movie in movies" :key="movie.id">
              <a :href="`https://www.themoviedb.org/movie/${movie.id}`">
                <img
                  :src="`https://image.tmdb.org/t/p/w342${movie.poster_path}`"
                  :alt="movie.title"
                />
                <span>{{ movie.title }}</span>
              </a>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <ContactCont />
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";
import { ref } from "vue";

import { Swiper, SwiperSlide } from "swiper/vue";
import { Navigation, Pagination, Autoplay } from "swiper";

import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
    Swiper,
    SwiperSlide,
  },

  setup() {
    const movies = ref([]);
    const top = ref([]);
    const search = ref("marvel");

    const SearchMovies = () => {
      fetch(
        `https://api.themoviedb.org/3/search/movie?api_key=9278d13f704ad0fe53c2263b692efd89&query=${search.value}`
      )
        .then((response) => response.json())
        .then((data) => {
          movies.value = data.results;
          search.value = "";
        })
        .catch((error) => console.log("error", error));
    };
    SearchMovies();

    const TopMovies = () => {
      fetch(
        `https://api.themoviedb.org/3/movie/popular?api_key=2da8ca399ff34f67831da4b85fa88dc7`
      )
        .then((response) => response.json())
        .then((result) => {
          top.value = result.results;
        })
        .catch((error) => console.log("error", error));
    };
    TopMovies();

    return {
      movies,
      search,
      top,
      SearchMovies,
      TopMovies,
      pagination: {
        clickable: true,
      },
      modules: [Navigation, Pagination, Autoplay],
    };
  },
};
</script>

<style lang="scss">
.movie__cont {
  background-color: var(--black);
}
.movie__list ul {
  display: flex;
  flex-wrap: wrap;

  li {
    flex: 1 1 23%;
    margin: 1%;

    img {
      border-radius: 0.4em;
    }

    span {
      -webkit-line-clamp: 2;
      -webkit-box-orient: vertical;
      color: var(--white);
      display: -webkit-box;
      font-family: SCoreDream;
      font-family: var(--subKor_font);
      overflow: hidden;
      padding-top: 10px;
      text-overflow: ellipsis;
    }
  }
}

.movie__search {
  background: var(--black);

  .container {
    position: relative;
  }

  h2 {
    color: var(--white);
    font-size: 40px;
    height: 0;
    text-indent: -9999px;
    width: 0;
  }

  input {
    background: var(--black);
    border: 2px solid var(--light_border);
    border-radius: 50px;
    color: #fff;
    color: var(--light_bg);
    margin: 0 1% 5%;
    padding: 1rem 3rem 1rem 2rem;
    width: 98%;
  }
  button {
    background: var(--white);
    border: 0;
    border-radius: 50%;
    color: var(--black);
    font-family: var(--subKor_font);
    font-size: 12px;
    height: 40px;
    position: absolute;
    right: 22px;
    top: 9px;
    transition: opacity 0.3s ease;
    width: 40px;
  }
}
.top_movies {
  height: auto;
  padding-bottom: 10vw;
  background: var(--black);
  height: 38vw;

  .title h1 {
    color: var(--white);
    font-family: "Saol";
    font-size: 4rem;
    text-align: center;
    margin-bottom: 2rem;
  }
  .swiper-slide {
    text-align: center;
    font-size: 18px;
    display: -webkit-box;
    display: -ms-flexbox;
    display: -webkit-flex;
    display: flex;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    -webkit-justify-content: center;
    justify-content: center;
    -webkit-box-align: center;
    -ms-flex-align: center;
    -webkit-align-items: center;
    align-items: center;
  }

  .swiper-pagination-bullet {
    background: var(--white);
  }
  .swiper-button-next,
  .swiper-button-prev {
    color: var(--white);
  }

  .swiper {
    width: 95%;
    height: 100%;
  }
  .top-item {
    width: 60%;
    margin-bottom: 4rem;
    img {
      object-fit: cover;
    }
  }
}
</style>
