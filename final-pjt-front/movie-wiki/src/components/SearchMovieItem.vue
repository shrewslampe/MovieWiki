<template>
  <div @click="hideSearchBar" class="route-title">
    <router-link
      :to="{
        name: 'movieDetail',
        params: { movieId: searchInfo.id },
      }"
      class="searh-title"
    >
      <li style="display: flex">
        <p class="font-gray">{{ start() }}</p>
        <p class="font-basic">{{ bold() }}</p>
        <p class="font-gray">{{ end() }}</p>
        <p class="font-medium-gray">
          ({{ searchInfo.released_date.slice(0, 4) }})
        </p>
      </li>
    </router-link>
  </div>
</template>

<script>
import { mapGetters, mapActions } from "vuex";
export default {
  name: "SearchMovieItem",
  data() {
    return {
      type: "",
    };
  },
  props: {
    searchInfo: {
      type: Object,
    },
    keyword: {
      type: String,
    },
  },
  methods: {
    ...mapActions(["setSearchBar"]),
    bold() {
      const start = this.searchInfo.title.indexOf(this.keyword);
      const end = start + this.keyword.length;
      let part = this.searchInfo.title.slice(start, end);
      if (this.searchInfo.title[end - 1] === " ") {
        part = this.searchInfo.title.slice(start, end) + "\u200b";
      }
      return part;
    },
    start() {
      const start = this.searchInfo.title.indexOf(this.keyword);
      let part = this.searchInfo.title.slice(0, start);

      if (this.searchInfo.title[start - 1] === " ") {
        part = this.searchInfo.title.slice(0, start) + "\u200b";
      }
      return part;
    },
    end() {
      const start = this.searchInfo.title.indexOf(this.keyword);
      const end = start + this.keyword.length;
      let part = this.searchInfo.title.slice(end, this.searchInfo.title.length);
      if (this.searchInfo.title[end] === " ") {
        part =
          "\u200b" +
          this.searchInfo.title.slice(end, this.searchInfo.title.length);
      }
      return part;
    },
    hideSearchBar() {
      this.setSearchBar(false);
    },
  },
  computed: {
    ...mapGetters(["searchBar"]),
  },
};
</script>

<style scoped>
li {
  width: 90vw;
  align-items: flex-start;
}

p {
  /* color: white; */
  font-size: 1.5rem;
}
.searh-title {
  text-decoration: none;
  height: 54.39px;
  margin-bottom: 0;
  margin-top: 16px;
  padding-bottom: 0;
}
.route-title {
  height: 50.39px;
  padding-bottom: 0;
}

@media (max-width: 950px) {
  p {
    font-size: 1.2rem;
  }
}

@media (max-width: 900px) {
  p {
    font-size: 1.1rem;
  }
}

@media (max-width: 800px) {
  p {
    font-size: 1rem;
  }
  .searh-title {
    height: 30px;
  }
  .route-title {
    height: 30px;
  }
}

@media (max-width: 600px) {
  p {
    font-size: 0.9rem;
  }
}

@media (max-width: 500px) {
  p {
    font-size: 0.8rem;
  }
}

@media (max-width: 400px) {
  p {
    font-size: 0.7rem;
  }
}
</style>
