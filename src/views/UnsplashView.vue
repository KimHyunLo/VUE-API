<template>
  <div>
    <HeaderCont />
    <TitleCont name1="unsplash" name2="api" />
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

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
  },

  setup() {
    const splashes = ref([]);
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

    return {
      splashes,
      search,
      SearchSplashes,
    };
  },
};
</script>

<style scoped lang="scss">
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
</style>
