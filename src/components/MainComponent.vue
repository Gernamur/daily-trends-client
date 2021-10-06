<template>
  <div class="main-component">
    <ul>
      <li v-for="feed in feeds" :key="feed._id">
        <div>
          <p>{{ feed.content }}</p>
          <span>{{ feed.mediaCompany }}</span>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "MainComponent",
  data() {
    return {
      feeds: [],
    };
  },
  async mounted() {
    let resource = `http://localhost:3000/feeds`
    this.feeds = (await axios.get(resource)).data;
    setInterval(async () => {
      this.feeds = (await axios.get(resource)).data;
    }, 5000);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.main-component > ul {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.main-component > ul > li {
  width: 300px;
  margin: 10px;
  padding: 5px;
  border-radius: 4px;
  background-color: rgba(0,0,0,0.05);
}

.main-component > ul > li > div > p {
  font-size: 14pt;
  text-align: left;
}
.main-component > ul > li > div > span {
  font-style: italic;
  font-size: 10pt;
  float: right;
}
</style>
