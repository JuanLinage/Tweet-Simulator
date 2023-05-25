<template>
  <div class="container">
    <h1 class="text-center">Lista de Tweets</h1>
    <div class="tweet" v-for="tweet in tweets" :key="tweet.id">
      <p class="tweet__title">{{ tweet.username }}</p>
      <p class="tweet__text">{{ tweet.tweet }}</p>
      <span>{{ formatDate(tweet.created) }}</span>
      <Close @click="deleteTweet(tweet.id)" />
    </div>
  </div>
</template>

<script>
import moment from "moment";
import "moment/locale/es";
import { Close } from "./icons/index";
import { deleteTweetApi } from "../api/tweet";

export default {
  props: {
    tweets: Array,
    reloadTweets: Function,
  },
  components: {
    Close,
  },

  setup(props) {
    const formatDate = (date) => {
      return moment(date).fromNow();
    };
    const deleteTweet = (idTweet) => {
      deleteTweetApi(idTweet);
      props.reloadTweets();
    };
    return {
      formatDate,
      deleteTweet,
    };
  },
};
</script>

<style lang="scss">
.tweet {
  position: relative;
  border: 1px solid gray;
  padding: 20px;
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
  align-content: center;

  p {
    margin: 0;
  }

  &__title {
    position: absolute;
    top: -12px;
    left: 10px;
    background-color: white;
    padding: 0 10px;
    font-weight: bold;
  }

  &__text {
    color: grey;
  }
  span {
    position: absolute;
    right: 10px;
    bottom: -9px;
    font-size: 12px;
    color: grey;
    background-color: white;
    padding: 0 20px;
    border: 1px solid grey;
  }
  svg {
    width: 20px;
    height: 20px;

    &:hover {
      cursor: pointer;
      color: red;
    }
  }
}
</style>
