<template>
  <div class="container">
    <div class="input-block">
      <label for="text">ticker</label>
      <input
        v-model="ticker"
        @keydown.enter="add"
        type="text"
        name="text"
        id="text"
      />
      <button @click="add">add</button>
    </div>
    <div v-if="tickers.length" class="list">
      <div
        v-for="i in tickers"
        v-bind:key="i.name"
        @click="sel = i"
        :class="sel == i ? ' chosen' : ''"
        class="list__item"
      >
        <p>{{ i.name }}</p>
        <button @click="del(i)">delete</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      ticker: "something texted by default",
      tickers: [{ name: "some" }, { name: "thing" }, { name: "maybe" }],
      sel: null,
    };
  },

  methods: {
    add() {
      this.tickers.push({
        name: this.ticker,
      });

      this.ticker = "";
    },
    del(i) {
      this.tickers = this.tickers.filter((el) => el != i);
    },
  },
};
</script>

<style>
p {
  margin: 0;
}
.container {
  margin: 16px;
  display: grid;
  gap: 24px;
}
.input-block {
  display: grid;
  gap: 6px;
  justify-items: start;
}
.list {
  display: grid;
  gap: 12px;

  padding: 24px;
  border: 1px solid grey;
}
.list__item {
  border: 1px solid grey;
  display: grid;
  gap: 6px;
  justify-items: start;

  padding: 8px;
}
.chosen {
  outline: 2px solid tomato;
}
</style>
