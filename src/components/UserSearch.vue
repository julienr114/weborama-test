<template>
  <div>
    <section class="hero is-medium is-primary">
      <div class="hero-body">
        <p class="title">Search user profil</p>
        <form>
          <input
            v-model="githubProfil"
            class="input"
            type="text"
            placeholder="Weborama"
          />
        </form>
      </div>
    </section>
    <div class="container">
      <article v-if="!loading && profil" class="media">
        <figure class="media-left">
          <p class="image is-64x64">
            <img :src="profil.avatar_url" />
          </p>
        </figure>
        <div class="media-content">
          <div class="content">
            <h1 class="title">{{ githubProfil }}</h1>
            <p>Created at {{ createdAt }}</p>
          </div>
        </div>
      </article>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import dayjs from "dayjs";
import debounce from "lodash.debounce";


export default {
  data() {
    return {
      githubProfil: null,
      profil: null,
      loading: false,
    };
  },

  computed: {
    createdAt () {
      if (this.profil && this.profil.created_at) {
        return dayjs(this.profil.created_at).format('DD MMMM YYYY')
      }
      return null
    }
  },

  watch: {
    githubProfil: debounce(function (value) {
      this.getProfil(value);
    }, 1000),
  },

  methods: {
    getProfil(param) {
      this.loading = true;
      axios
        .get(`https://api.github.com/users/${param}`)
        .then((res) => {
          this.profil = res.data;
          this.loading = false;
        })
        .catch((err) => {
          console.error(err);
          this.loading = false;
        });
    },

  },
};
</script>
