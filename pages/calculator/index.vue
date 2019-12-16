<template lang="pug">
  .calc 
    h1.title Калькулятор
    form
      input.input(
        type="text"
        v-for="item, index in items"
        :key="index"
        v-model="item.data"
        @input="inputText(item.data, index)"
      )
    .sum
      span Сумма: &nbsp;
      span(
        v-text="sum"
      )
</template>

<script>
export default {
  data() {
    return {
      items: [
        {
          data: null
        }
      ]
    };
  },

  computed: {
    sum() {
      let sum = 0;
      for (let item in this.items) {
        let currentData = this.items[item].data;

        sum += Number(currentData);
      }
      return sum;
    }
  },

  methods: {
    inputText(_data, _index) {
      let curLength = this.items.length;
      if (_data.length > 0 && curLength === _index + 1) {
        this.items.push({
          data: ""
        });
      } else if (_data.length === 0) {
        this.items.splice(_index, 1);
      }
    }
  }
};
</script>

<style lang="scss">
.calc {
  max-width: 1000px;
  width: 100%;
  margin: 0 auto;
  padding: 3rem;
  box-sizing: border-box;
  text-align: center;

  .input {
    margin-bottom: 1rem;
  }

  & > .title {
    margin-bottom: 2rem;
  }
  form {
    display: flex;
    flex-direction: column;
  }
}
</style>

