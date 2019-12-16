<template lang="pug">
  .user 
    .title(
      v-if="currentStep !== 'phone'"
    ) Введите данные:
    .form
      .block(
        v-for="item, index in user"
        :key="index"
        v-if="currentStep === item.name"
        :class="[{'-modal': currentStep === 'phone'}]"
      )
        label(
          :for="item.name"
          v-text="item.title"
        )
        input(
          :id="item.name"
          v-model="item.text"
        )
        button.button--grey(
          @click="saveData"
          v-if="currentStep === 'phone'"
        ) Закончить
    button.button--grey(
      @click="nextStep"
      v-if="currentStep !== 'phone'"
    ) Далее
</template>

<script>
import { mapMutations } from "vuex";
export default {
  data() {
    return {
      currentStep: "",
      count: 0,
      user: [
        {
          title: "Фамилия",
          text: "",
          name: "lastName"
        },
        {
          title: "Имя",
          text: "",
          name: "firstName"
        },
        {
          title: "Телефон",
          text: "",
          name: "phone"
        }
      ]
    };
  },

  computed: {},

  methods: {
    ...mapMutations(["SAVE_USER_DATA"]),

    nextStep() {
      this.currentStep = this.user[this.count].name;
      this.count++;
    },

    async saveData() {
      await this.SAVE_USER_DATA(this.user);
      $nuxt.$router.push("/userData");
    }
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
  .form {
    & > .block {
      display: flex;
      margin: 1rem 1rem 1rem 0;
      & > label {
        margin-right: 0.5rem;
      }
    }
    & > .-modal {
      width: 20vw;
      height: 20vh;
      position: absolute;
      display: flex;
      align-items: center;
      justify-content: center;
      margin: 0;
      top: 50%;
      left: 50%;
      transform: translateY(-50%) translateX(-50%);
      background: rgba(#000, 0.3);
    }
  }
}
</style>

