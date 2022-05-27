<template>
    <v-chip @click="test"><slot></slot></v-chip>
</template>

<script>

export default {
  name: "EntityMark",

  data: () => ({
    test() {
        console.log("Hello World!")
    }
  }),

};

</script>
