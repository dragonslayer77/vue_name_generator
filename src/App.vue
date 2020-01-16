
<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import List from "./components/List";

export default {
  name: "app",
  components: {
    List
  },
  data: function() {
    return {
      prefixes: ["Air", "Jet", "Flight"],
      sufixes: ["Hub", "Station", "Mart"]
    };
  },
  methods: {
    addPrefix(prefix) {
      this.prefixes.push(prefix);
    },
    addSufix(sufix) {
      this.sufixes.push(sufix);
    },
    deletePrefix(prefix) {
      this.prefixes.splice(this.prefixes.indexOf(prefix), 1);
    },
    deleteSufix(sufix) {
      this.sufixes.splice(this.sufixes.indexOf(sufix), 1);
    }
  },
  computed: {
    domains() {
      console.log("generating domains...");
      const domains = [];
      for (const prefix of this.prefixes) {
        for (const sufix of this.sufixes) {
          const name = prefix + sufix;
          const url = name.toLowerCase();
          domains.push({
            name,
            link: `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`
          });
        }
      }
      return domains;
    }
  }
};
</script>



<template>
  <div>
    <div id="slogan" class="text-center">
      <h1>Name Generator</h1>
      <br />
      <h6 class="text-secondary">Name generator made in Vue.js</h6>
    </div>
    <div id="main">
      <div class="container">
        <div class="row">
          <List v-bind:items="prefixes" name="Prefixes" v-on:addItem="addPrefix" v-on:deleteItem="deletePrefix" />
          <List v-bind:items="sufixes" name="Sufixes" v-on:addItem="addSufix" v-on:deleteItem="deleteSufix" />
        </div>
        <br />
        <h5>
          Domains
          <span class="badge badge-info">{{domains.length}}</span>
        </h5>
        <div class="card">
          <div class="card-body">
            <ul class="list-group">
              <li class="list-group-item" v-for="domain in domains" v-bind:key="domain.name">
                <div class="row">
                  <div class="col-md">{{domain.name}}</div>
                  <div class="col-md text-right">
                    <a class="btn btn-info" v-bind:href="domain.link" target="_blank">
                      <span class="fa fa-shopping-cart"></span>
                    </a>
                  </div>
                </div>
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>



<style>
#slogan {
  margin-top: 30px;
  margin-bottom: 30px;
}
#main {
  background-color: #f1f1f1;
  padding-top: 30px;
  padding-bottom: 30px;
}
</style>
