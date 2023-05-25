<template>
  <Menu :openCloseForm="openCloseForm" :showForm="showForm" />
  <TweetForm
    :showForm="showForm"
    :reloadTweets="reloadTweets"
    :openCloseForm="openCloseForm"
  />
  <TweetList :tweets="tweets" :reloadTweets="reloadTweets" />
</template>

<script>
import { ref } from "vue";
import Menu from "./components/Menu.vue";
import TweetForm from "./components/TweetForm.vue";
import TweetList from "./components/TweetList.vue";
import useFormTweet from "./Hooks/useFormTweet";
import { getTweetsApi } from "./api/tweet";

export default {
  components: {
    Menu,
    TweetForm,
    TweetList,
  },
  setup() {
    let tweets = ref(getTweetsApi().reverse());
    const reloadTweets = () => {
      tweets.value = getTweetsApi().reverse();
    };

    return {
      tweets,
      ...useFormTweet(),
      reloadTweets,
    };
  },
};
</script>

<style lang="scss"></style>
