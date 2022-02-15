<template>
  <div class="hello">
    <v-container>
      <v-btn class="mr-2" @click="isHttps = !isHttps">https toggle</v-btn>
      isHTTPS: {{ isHttps }}

      <v-text-field label="Main input" v-model="toIpfs"></v-text-field>
      <v-btn color="success" @click="AddToIpfs">send to ipfs</v-btn>
      <v-divider></v-divider>

      <v-text-field label="Hash input" v-model="hash"></v-text-field>
      <v-btn color="success" @click="GetFromIpfs">Get data</v-btn> <br /><br />
      <v-btn color="success" @click="getStatFromIpfs">Get Stats</v-btn>
    </v-container>
  </div>
</template>

<script>
const IPFS = require("ipfs-mini");
const ipfs = new IPFS({
  host: "ipfs.xinfin.network",
  port: 443,
  protocol: "https",
});
const ipfs2 = new IPFS({
  host: "ipfs.xinfin.network",
  port: 443,
});

export default {
  props: {
    msg: String,
  },
  data: () => ({
    toIpfs: "",
    hash: "",

    isHttps: true,
  }),
  methods: {
    AddToIpfs() {
      console.log("AddToIpfs", this.toIpfs, "isHttps", this.isHttps);

      if (this.isHttps)
        ipfs.add(this.toIpfs).then(console.log).catch(console.log);
      else ipfs2.add(this.toIpfs).then(console.log).catch(console.log);
    },
    GetFromIpfs() {
      console.log("GetFromIpfs", this.hash, "isHttps", this.isHttps);

      if (this.isHttps)
        ipfs.cat(this.hash).then(console.log).catch(console.log);
      else ipfs2.cat(this.hash).then(console.log).catch(console.log);
    },
    getStatFromIpfs() {
      console.log("getStatFromIpfs", this.hash, "isHttps", this.isHttps);

      if (this.isHttps)
        ipfs.stat(this.hash).then(console.log).catch(console.log);
      else ipfs2.stat(this.hash).then(console.log).catch(console.log);
    },
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
</style>
