<template>
  <div class="user-info bg-medium-gray">
    <user-profile-image
      class="user-info__image"
      width="100px"
      height="100px"
      :image="image"
    ></user-profile-image>
    <div class="user-info__content">
      <div class="user-info__content__title">
        <p class="font-basic">{{ userInfoDetail.nickname }}</p>
        <button
          class="bg-icon-green"
          @click="showUserChangeModal"
          v-if="isSelf"
        >
          회원 정보 수정
        </button>
      </div>
      <div class="user-info__content__activity">
        <p>| 내가 찜한 영화: {{ likeMovies }} 개</p>
        <p>| 내 게시글: {{ myArticle }}개</p>
        <p>| 내 댓글: {{ myComment }}개</p>
        <p>| 내 평가: {{ myReview }}개</p>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import UserProfileImage from "@/components/UserProfileImage.vue";
export default {
  components: { UserProfileImage },
  name: "UserInfo",
  computed: {
    ...mapGetters(["userInfoDetail", "isSelf", "userProfile"]),
    image() {
      if (this.isSelf) {
        return this.userProfile.image;
      } else {
        return this.userInfoDetail.profile_image;
      }
    },
    likeMovies() {
      const movies = this?.userInfoDetail?.like_movies;
      return movies?.length;
    },
    myArticle() {
      const articles = this?.userInfoDetail?.article;
      return articles?.length;
    },
    myComment() {
      const comments = this?.userInfoDetail?.comment;
      return comments?.length;
    },
    myReview() {
      const review = this?.userInfoDetail?.review;
      return review?.length;
    },
  },
  methods: {
    showUserChangeModal() {
      this.$emit("show-user-change-modal", true);
    },
  },
};
</script>

<style scoped>
.user-info {
  width: 80%;
  padding: 3em;
  border-radius: 0.4em;
  display: flex;
  align-items: center;
  gap: 3em;
}

@media (max-width: 652px) {
  .user-info {
    flex-direction: column;
  }
}

.user-info__content {
  display: flex;
  flex-direction: column;
  gap: 2em;
}

.user-info__content__title {
  display: flex;
  flex-wrap: wrap;
  gap: 2em;
}

.user-info__content__activity {
  display: flex;
  gap: 2em;
  flex-wrap: wrap;
}

.user-info__content__title > p {
  font-size: 1.7em;
  font-weight: 500;
}

.user-info__content__title > button {
  border-radius: 0.4em;
  color: white;
  font-size: 0.8em;
  padding: 0.4em;
}

.user-info__content__activity > p {
  color: #b9bbbe;
  font-size: 1.3em;
}
</style>
