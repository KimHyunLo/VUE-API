<template>
  <div>
    <HeaderCont />
    <section className="main__cont">
      <div class="main__inner">
        <ul>
          <li v-for="title in titles" v-bind:key="title.text">
            {{ title.text }}
          </li>
        </ul>
      </div>
    </section>
    <FooterCont />
  </div>
</template>

<script>
import HeaderCont from "@/components/HeaderCont.vue";
import FooterCont from "@/components/FooterCont.vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
  },

  data: function () {
    return {
      titles: [
        { text: "we provide" },
        { text: "visual coding" },
        { text: "solutions" },
        { text: "for your web" },
      ],
    };
  },
};
</script>

<style scoped lang="scss">
.main__cont {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: var(--black);

  .main__inner {
    font-size: 10vw;
    line-height: 0.85;
    font-family: var(--main_font);
    color: var(--white);
    text-transform: uppercase;
  }
}

// main Animation
// .main__list > div {
//   opacity: 0;
//   transform: translateY(100px);
// }
</style>
