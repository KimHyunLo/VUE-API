<template>
  <div>
    <HeaderCont />
    <TitleCont name1="Youtube" name2="api" />
    <div className="youtube__swiper">
      <div className="top-slide">
        <span className="title">
          <h1>Popular Videos</h1>
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
          <swiper-slide v-for="vid in top" :key="vid">
            <div className="top-item">
              <a :href="`https://www.youtube.com/watch?v=${vid.id}`">
                <img
                  :src="vid.snippet.thumbnails.medium.url"
                  :alt="vid.snippet.title"
                />
                <p>{{ vid.snippet.title }}</p>
              </a>
            </div>
          </swiper-slide>
        </swiper>
      </div>
    </div>
    <div className="youtube__search">
      <form @submit.prevent="SearchYoutubes()">
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
    <div className="youtube__cont">
      <div className="container">
        <div className="youtube__inner">
          <ul>
            <div className="youtube__list">
              <ul>
                <li v-for="youtube in youtubes" :key="youtube.id.videoId">
                  <a
                    :href="`https://www.youtube.com/watch?v=${youtube.id.videoId}`"
                  >
                    <img
                      :src="youtube.snippet.thumbnails.medium.url"
                      :alt="youtube.snippet.title"
                    />
                    <p>{{ youtube.snippet.title }}</p>
                  </a>
                </li>
              </ul>
            </div>
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
    const youtubes = ref([]);
    // const top = ref([]);
    const top = ref([1, 2, 3, 4, 5, 6, 7, 8, 9, 10]);
    const search = ref("marvel");

    const SearchYoutubes = () => {
      fetch(
        `https://youtube.googleapis.com/youtube/v3/search?part=snippet&q=${search.value}&key=AIzaSyA8SlPA6kqX0OihTlnTbSNz8HL0gULdzB0&maxResults=28&type=video`
      )
        .then((response) => response.json())
        .then((data) => {
          youtubes.value = data.items;
          search.value = "";
        })
        .catch((error) => console.log("error", error));
    };
    SearchYoutubes();

    const TopYoutubes = () => {
      fetch(
        `https://youtube.googleapis.com/youtube/v3/videos?part=snippet&chart=mostPopular&regionCode=KR&maxResults=10&key=AIzaSyA8SlPA6kqX0OihTlnTbSNz8HL0gULdzB0`
      )
        .then((response) => response.json())
        .then((result) => {
          top.value = result.items;
        })
        .catch((error) => console.log("error", error));
    };
    TopYoutubes();

    return {
      youtubes,
      top,
      search,
      SearchYoutubes,
      TopYoutubes,
      pagination: {
        clickable: true,
      },
      modules: [Navigation, Pagination, Autoplay],
    };
  },
};
</script>

<style lang="scss">
.youtube__cont {
  background-color: var(--black);
}
.youtube__list {
  ul {
    display: flex;
    flex-wrap: wrap;

    li {
      flex: 1 1 23%;
      margin: 1%;

      img {
        border-radius: 0.4em;
      }
      p {
        color: var(--white);
        font-family: var(--subKor_font);
        padding-top: 10px;
        overflow: hidden;
        text-overflow: ellipsis;
        display: -webkit-box;
        -webkit-line-clamp: 2;
        -webkit-box-orient: vertical;
      }
    }
  }
}

.youtube__search {
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

@media (max-width: 800px) {
  .youtube__list ul li {
    flex: 1 1 43%;
  }
}

.youtube__swiper {
  .top-slide {
    height: auto;
    padding-bottom: 10vw;
    background: var(--black);
    height: 38vw;

    .title h1 {
      color: var(--white);
      font-family: "Saol";
      font-size: 4rem;
      text-align: center;
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
      width: 75%;
      height: 60%;
      margin-bottom: 2rem;
      p {
        text-align: left;
        margin-top: 1rem;
        color: var(--white);
      }
      img {
        border: 1px solid var(--black);
        object-fit: cover;
      }
    }
  }
}
.btn__list {
  background: var(--black);
  width: 100%;
  padding-bottom: 4rem;
  ul {
    display: flex;
    justify-content: center;
    align-items: center;

    .search {
      color: var(--black);
      background: var(--white);
      padding: 0.5rem 1.5rem;
      margin: 0 1rem;
      border-radius: 2rem;
      cursor: pointer;
    }
  }
}
</style>
