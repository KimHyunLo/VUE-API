<template>
  <div>
    <HeaderCont />
    <TitleCont name1="reference" name2="api" />
    <section className="refer__cont">
      <div className="container">
        <div className="refer__inner">
          <h2>CSS</h2>
          <ul className="refer__list">
            <li v-for="ref in refs" :key="ref.id">
              <a href="#">
                <span className="num">{{ ref.id }}</span>
                <span className="title">{{ ref.title }}</span>
                <span className="desc">{{ ref.desc }}</span>
                <span className="use">{{ ref.use }}</span>
              </a>
            </li>
          </ul>
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
import { ref } from "vue";

export default {
  components: {
    HeaderCont,
    FooterCont,
    TitleCont,
    ContactCont,
  },

  setup() {
    const refs = ref([]);

    const References = () => {
      fetch(
        "https://webstoryboy.github.io/react2022/src/assets/json/refer.json"
      )
        .then((res) => res.json())
        .then((data) => {
          refs.value = data.data.htmlRefer;
        })
        .catch((error) => console.log("error", error));
    };
    References();

    return {
      refs,
      References,
    };
  },
};
</script>

<style scoped lang="scss">
.refer__cont {
  background-color: var(--black);
  min-height: 100vh;
}
.refer__inner {
  h2 {
    color: var(--white);
    font-size: 2rem;
    margin-bottom: 1rem;
  }
}

.refer__list {
  border-top: 2px solid var(--light_bg);
  border-bottom: 1px solid var(--light_bg);

  a {
    display: block;
    color: var(--white);
    display: flex;
    align-items: center;
    justify-content: space-between;
    border-bottom: 1px solid var(--light_bg);
    padding: 1.3rem 0;
    transition: all 0.3s;
    font-family: var(--subKor_font);

    &:hover {
      background: var(--light_bg);
      color: var(--black);
    }
    span {
      display: inline-block;
    }
    span:nth-child(1) {
      width: 6%;
      text-align: center;
    }
    span:nth-child(2) {
      width: 20%;
    }
    span:nth-child(3) {
      width: 64%;
    }
    span:nth-child(4) {
      width: 10%;
      text-align: center;
    }
  }
}

.refer__table {
  margin-top: 200px;
  color: var(--white);
  font-family: var(--subKor_font);

  h3 {
    font-size: 3rem;
  }
  p {
    background-color: var(--light_bg);
    color: var(--black);
    padding: 1.4em;
  }

  .table {
    color: var(--white);
    font-family: var(--subKor_font);
    border: 1px solid var(--light_bg);
    margin-top: 0.5em;

    th,
    td {
      font-weight: normal;
      padding: 1em;
      border-bottom: 1px solid var(--light_bg);
      border-left: 1px solid var(--light_bg);
    }
  }
}

.refer__cont.light {
  background-color: var(--light_bg);

  .refer__inner {
    h2 {
      color: var(--black);
    }

    table {
      border-color: var(--black);
      color: var(--black);

      td {
        border-color: var(--black);
      }
    }
  }
}

//???????????????
// .refer__inner {
//     opacity: 0;
//     transform: translateY(50px);
// }
</style>
