<template>
  <Menu :openCloseForm="openCloseForm" :showForm="showForm" />
  <TweetForm :showForm="showForm" :openCloseForm="openCloseForm" :reloadTweets="reloadTweets" />
  <TweetList :tweets="tweets" :reloadTweets="reloadTweets" />
</template>

<script>
import { ref } from "vue";
import Menu from "./components/MenuView.vue";
import TweetForm from "./components/TweetForm.vue";
import TweetList from "./components/TweetList.vue";
import useFormTweet from "./hooks/useFormTweet";
import { getTweetsApi } from "./api/tweet";

export default {
  name: "App",
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
      ...useFormTweet(),
      tweets,
      reloadTweets,
    };
  },
};
</script>

<style lang="scss"></style>
