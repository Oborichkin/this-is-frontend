<template>
  <v-main>
    <v-container style="max-width: 960px">
      <v-row>
        <h1>Search</h1>
      </v-row>
      <v-row>
        <v-text-field v-model="searchQuery" outlined clearable type="text">
        </v-text-field>
        <v-btn
          class="mx-2"
          fab
          dark
          color="primary"
          @click="startSearch"
          @keyup.enter="startSearch"
        >
          <v-icon dark> mdi-magnify </v-icon>
        </v-btn>
      </v-row>

      <v-row v-for="(result, index) in searchResults" :key="index">
        <v-card class="searchResult" elevation="2" outlined min-width="100%">
          <v-card-title>{{ result.ch.name }}</v-card-title>
          <v-card-subtitle>
            <v-chip class="ma-2" color="primary">UA </v-chip>
            <v-chip class="ma-2" color="red">MUST </v-chip>
            <v-chip class="ma-2" color="secondary">increment </v-chip>
            <v-chip class="ma-2" color="primary">CSeq value</v-chip>
          </v-card-subtitle>
          <v-card-text>{{ result.sent.text }}</v-card-text>
          <v-card-actions>
            <v-btn text>
              Перейти к тексту
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-row>
    </v-container>
  </v-main>
</template>

<script>
import axios from "axios";

export default {
  data: () => ({
    searchQuery: "",
    searchResults: [],
    errors: [],
  }),

  methods: {
    startSearch() {
      axios
        .get(`http://localhost:8000/entity`, {
          params: { name: this.searchQuery },
        })
        .then((response) => {
          this.searchResults = response.data;
        })
        .catch((e) => {
          this.errors.push(e);
        });
    },
  },
};
</script>