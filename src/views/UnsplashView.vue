<template>
  <div>
    <HeaderCont />
    <TitleCont name1="unsplash" name2="api" />
    <div className="random-slide">
      <span className="title">
        <h1>Random Splash</h1>
      </span>
      <swiper
        :slidesPerView="3"
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
            <a :href="vid.links.html">
              <img :src="vid.urls.regular" :alt="vid.id" />
            </a>
          </div>
        </swiper-slide>
      </swiper>
    </div>
    <div className="splash__search">
      <form @submit.prevent="SearchSplashes()">
        <div className="container">
          <h2>검색하기</h2>
          <input
            id="search"
            type="search"
            placeholder="검색하세요."
            v-model="search"
          />
          <button type="submit">검색</button>
        </div>
      </form>
    </div>
    <div className="splash__cont">
      <div className="container">
        <div className="splash__list">
          <ul>
            <li v-for="splash in splashes" :key="splash.id">
              <a :href="`https://unsplash.com/photos/${splash.id}`">
                <img :src="splash.urls.regular" :alt="splash.id" />
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
    const splashes = ref([]);
    const top = ref([]);
    const search = ref("marvel");

    const SearchSplashes = () => {
      fetch(
        `https://api.unsplash.com/search/photos?query=${search.value}&client_id=_Qj8pAEH3PNaxSoZd9sPXo5pmx7noH38BI4nmYwxlSI&per_page=30`
      )
        .then((response) => response.json())
        .then((data) => {
          splashes.value = data.results;
          search.value = "";
        })
        .catch((error) => console.log("error", error));
    };
    SearchSplashes();

    const RandomSplash = () => {
      fetch(
        `https://api.unsplash.com/photos/random?client_id=_Qj8pAEH3PNaxSoZd9sPXo5pmx7noH38BI4nmYwxlSI&count=10`
      )
        .then((response) => response.json())
        .then((result) => {
          top.value = result;
        })
        .catch((error) => console.log("error", error));
    };
    RandomSplash();

    return {
      splashes,
      search,
      SearchSplashes,
      top,
      RandomSplash,
      pagination: {
        clickable: true,
      },
      modules: [Navigation, Pagination, Autoplay],
    };
  },
};
</script>

<style lang="scss">
.splash__cont {
  background-color: var(--black);
}
.splash__list ul {
  width: 100%;
  columns: 4;
  column-gap: 20px;
}

.splash__list ul img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  margin-bottom: 20px;
  border-radius: 5px;
  cursor: pointer;
  background: #f9f9f9;
}

.splash__search {
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
    color: #f0eeeb;
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
.random-slide {
  height: auto;
  background: var(--black);
  padding-bottom: 5rem;

  .title h1 {
    color: var(--white);
    font-family: "Saol";
    font-size: 4rem;
    text-align: center;
  }

  .swiper {
    width: 95%;
    height: 30vw;
    display: flex;
    align-items: center;
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

  .top-item {
    width: 75%;
    height: 80%;
    border: 1px solid var(--white);
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
}
</style>
