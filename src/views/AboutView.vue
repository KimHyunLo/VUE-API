<template>
  <div>
    <HeaderCont />
    <TitleCont name1="about" name2="api" />
    <section className="about__cont">
      <div className="container">
        <div className="about__inner">
          <li v-for="text in aboutText" :key="text.title">
            <div className="about">
              <div className="about__txt">
                <h3>{{ text.title }}</h3>
                <p>{{ text.desc }}</p>
              </div>
              <div className="about__img">
                <img :src="text.img" :alt="text.title" />
              </div>
            </div>
          </li>
        </div>
      </div>
    </section>
    <ContactCont />
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";
import TitleCont from "@/components/TitleCont.vue";
import ContactCont from "@/components/ContactCont.vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
  },
  data: function () {
    return {
      aboutText: [
        {
          title: "유튜브 API",
          desc: "유튜브에서 제공하는 API를 이용해서 작업했습니다.",
          img: "https://images.unsplash.com/photo-1663183538127-82173c57b25e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1887&q=80",
        },
        {
          title: "TMDB API",
          desc: "TMDB에서 제공하는 API를 이용해서 작업했습니다.",
          img: "https://images.unsplash.com/photo-1663431263825-b78496c2a7af?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80",
        },
        {
          title: "Unsplash API",
          desc: "Unsplash에서 제공하는 API를 이용해서 작업했습니다.",
          img: "https://images.unsplash.com/photo-1663431905837-09cf339461ce?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1907&q=80",
        },
      ],
    };
  },
};
</script>

<style scoped lang="scss">
.about__cont {
  background-color: var(--black);
}

.about__inner {
  .about {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    padding-bottom: 30vh;
    color: var(--white);
    font-family: var(--kor_font);

    .about__img {
      flex: 0 0 64%;
    }

    .about__txt {
      flex: 0 0 32%;
      text-align: justify;

      h3 {
        margin-bottom: 30px;
        font-size: 1.4rem;
        line-height: 1;
      }

      p {
        font-size: 1rem;
        line-height: 1.6;
      }
    }

    &:nth-child(even) {
      flex-direction: row-reverse;
    }
  }
}
</style>
