<template>
  <div class="hello">
    <input type="textbox" v-model="title" class="inputBox" />
    <br />
    <button class="mt-top mt-right" @click="fetchPrev">Previous</button>
    <button class="mt-top" @click="fetchNext">Next</button>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "HelloWorld",
  data() {
    return {
      title: "",
      nextID: 1,
      currentId: 1,
    };
  },
  methods: {
    fetchNext() {
      if (!this.nextID) {
        this.nextID = 1;
      }
      let addUrl =
        "https://jsonplaceholder.typicode.com/posts/" + this.nextID + "";
      axios
        .get(addUrl)
        .then((response) => {
          let data = response.data;
          this.title = data.title;
          this.currentID = data.id;
          this.nextID = data.id + 1;
        })
        .catch((e) => {
          console.log(e);
        });
    },
    fetchPrev() {
      const varSet = this.currentID - 1;
      let addUrl1 = "https://jsonplaceholder.typicode.com/posts/" + varSet + "";
      axios
        .get(addUrl1)
        .then((response) => {
          console.log(response);
          let data = response.data;
          this.title = data.title;
          this.nextID = data.id + 1;
          this.currentID = data.id;
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },
  created() {
    this.fetchNext();
  },
};
</script>

<style scoped>
.mt-top {
  margin-top: 10px;
}
.mt-right {
  margin-right: 10px;
}
.inputBox {
  width: 200px;
  height: 80px;
}
</style>
