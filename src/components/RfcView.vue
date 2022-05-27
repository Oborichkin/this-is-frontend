<template>
  <div>
    <v-navigation-drawer app>
      <v-list dense>
        <v-list-item-group>
          <a :href="'#' + ch.title" v-for="(ch, i) in rfc.chapters" :key="i">
            <v-list-item>
              {{ ch.title }}
            </v-list-item>
          </a>
        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
    <v-main>
      <v-container style="max-width: 960px">
        <h1>{{ rfc.title }}</h1>
        <div v-for="ch in rfc.chapters" v-bind:key="ch">
          <a :id="ch.title"></a>
          <h2>{{ ch.title }}</h2>
          <p v-for="section in ch.sections" v-bind:key="section">
            <Highlighter class="my-highlight"
              v-if="section.type == 'text'" 
              highlightClassName="highlight"
              :highlightTag="mark"
              :searchWords="entities"
              :autoEscape="true"
              :textToHighlight="section.text"/>
            <span class="rfc-scheme" v-else style="white-space: pre">{{
              section.text
            }}</span>
          </p>
        </div>
      </v-container>
    </v-main>
  </div>
</template>

<script>
import axios from "axios";
import Highlighter from 'vue-highlight-words'
import EntityMark from './Entity.vue'

export default {
  name: "RfcView",

  components: {
    Highlighter
  },

  data: () => ({
    rfc: null,
    entities: null,
    errors: [],
    mark: EntityMark,
    highlightRequests(text) {
      for (const entity of this.entities) {
        text = text.replace(` ${entity} `, ` <span @click="test" class='entity'>${entity}</span> `)
      }
      return text
    }
  }),

  created() {
    axios
      .get("http://localhost:8000/")
      .then((response) => {
        this.rfc = response.data;
      })
      .catch((e) => {
        this.errors.push(e);
      });
    axios
      .get("http://localhost:8000/entities")
      .then((response) => {
        this.entities = response.data;
      })
      .catch((e) => {
        this.errors.push(e);
      });
  },
};

</script>
