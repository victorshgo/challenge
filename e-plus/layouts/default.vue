<template>
  <v-app>
    <v-toolbar>
      <v-img class="logo"></v-img>
      <v-spacer/>
      <v-icon class="mr-5">search</v-icon>
      <v-icon class="mr-5">person</v-icon>
      <v-menu :close-on-content-click="false" :max-width="400" offset-x>
        <template v-slot:activator="{ on }">
          <v-badge color="success">
            <template v-slot:badge>
              <span>{{ json.cart.length }}</span>
            </template>
            <v-icon v-on="on">shopping_cart</v-icon>
          </v-badge>
        </template>
        <v-card>
          <v-list>
            <v-layout v-for="(item, index) of json.cart" v-bind:key="index" row wrap>
              <v-flex class="pa-3" xs4>
                <v-img :src="item.image"></v-img>
              </v-flex>
              <v-flex class="pa-3" xs8>
                <p class="mb-3" v-text="item.name"></p>
                <span style="float: left"><strong>QTD: {{ item.quantity }}</strong></span>
                <span style="float: right" class="price" v-text="item.bestPriceFormated"></span>
              </v-flex>
            </v-layout>
          </v-list>
          <v-divider></v-divider>
          <v-list>
            <span class="ml-4 title-price" style="float: left"><strong>TOTAL: </strong></span>
            <span class="mr-4 message-price" style="float: right">R${{ total }}</span>
          </v-list>
          <v-card-actions>
            <v-btn color="success" class="finalize-purchase">Finalize Purchase</v-btn>
          </v-card-actions>
        </v-card>
      </v-menu>
    </v-toolbar>
    <v-container>
      <v-container>
        <nuxt/>
      </v-container>
    </v-container>
  </v-app>
</template>

<script>
import json from "../static/json/products.json";

export default {
  data() {
    return {
      total: 0,
      json: null,
      title: "Vuetify.js"
    };
  },

  created() {
    this.json = json;
    this.total = json.cart.map(el => el.bestPrice).reduce((back, next) => back + next);
  }
};
</script>

<style scoped>
.logo {
  height: auto;
  max-width: 20% !important;
  content: url("../static/images/agencia-eplus-n-logo.png");
}

.finalize-purchase {
  width: 100%;
  margin: 0 !important;
}

.v-list {
  overflow-y: auto;
  max-height: 450px !important;
}

.title-price {
  font-size: 15pt;
}

.message-price {
  color: green;
  font-size: 15pt;
}
</style>
