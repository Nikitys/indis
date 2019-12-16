<template lang="pug">
  .user 
    .title Данные пользователя:
    .form
      .block(
        v-for="item, index in user"
        :key="index"
      )
        .label(
          v-text="item.title"
        )
        .text(
          v-text="item.text"
        )


</template>

<script>
import { mapGetters } from "vuex";

export default {
  computed: {
    ...mapGetters(["user"])
  }
};
</script>

<style lang="scss">
.user {
  max-width: 1000px;
  width: 100%;
  margin: 0 auto;
  padding: 3rem;
  box-sizing: border-box;
  .label {
    margin-right: 1rem;
  }
}
</style>

