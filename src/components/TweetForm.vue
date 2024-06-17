<template>
  <div class="tweet-form container" :class="{ open: showForm }">
    <form @submit.prevent="sendTweet">
      <input class="form control" placeholder="Tu nombre" v-model="username" />
      <textarea placeholder="Escribe tu email" rows="3" class="form-control" v-model="tweet"></textarea>
      <button type="submit" class="btn btn-primary">Enviar Tweet</button>
    </form>
  </div>
</template>

<script>
import { ref } from "vue";
import { saveTweetApi } from "../api/tweet";

export default {
  props: {
    showForm: Boolean,
    reloadTweets: Function,
    openCloseForm: Function,
  },
  setup(props) {
    let username = ref("");
    let tweet = ref("");

    const sendTweet = () => {
      if (!username.value || !tweet.value) return;

      saveTweetApi(username.value, tweet.value);
      tweet.value = "";
      username.value = "";
      props.reloadTweets();
      props.openCloseForm();
    };
    return { sendTweet, username, tweet };
  },
};
</script>

<style lang="scss" scoped>
.tweet-form {
  margin-top: 20px;
  height: 0;
  overflow: hidden;

  &.open {
    height: auto;
  }

  form {
    margin-bottom: 50px;

    input {
      margin-bottom: 10px;
    }

    button {
      width: 100%;
      margin-top: 10px;
    }
  }
}
</style>
