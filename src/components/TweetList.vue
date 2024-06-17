<template>
  <div class="container">
    <h1 class="text-center mb-4">Lista de Tweets</h1>
    <p v-if="!tweets.length">No hay Tweets</p>
    <div class="tweet" v-for="tweet in tweets" :key="tweet.id">
      <p class="tweet_title">{{ tweet.username }}</p>
      <p class="tweet_text">{{ tweet.tweet }}</p>
      <span>{{ formatDate(tweet.createdAt) }}</span>
      <Close @click="deleteTweet(tweet.id)" />
    </div>
  </div>
</template>

<script>
import moment from "moment";
import "moment/locale/es";
import { Close } from "./Icons/index";
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
  border: 1px solid #ccc;
  padding: 20px;
  margin-bottom: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;

  p {
    margin: 0;
  }

  &_title {
    position: absolute;
    top: -12px;
    left: 10px;
    background-color: white;
    padding: 0 10px;
    font-weight: bold;
  }

  &_text {
    color: grey;
  }

  span {
    position: absolute;
    right: 10px;
    font-size: 12px;
    color: grey;
    background-color: white;
    padding: 0 20px;
    bottom: -9px;
    border: 1px solid #ccc;
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
