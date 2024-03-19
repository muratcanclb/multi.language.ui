<template>
    <select @change="updateLanguage()" v-model="$i18n.locale">
      <option v-for="(locale, i) in locales" :key="`locale-${i}`" :value="locale">
        {{ locale.toUpperCase() }}
      </option>
    </select>
  </template>
  
  <script>
  export default {
    name: "LocaleSwitcher",
    data() {
      return { locales: ["ar","tr", "en"] };
    },
    methods: {
      updateLanguage() {
        sessionStorage.setItem("locale", this.$i18n.locale);
      },
    },
    mounted() {
      if (sessionStorage.getItem("locale")) {
        this.$i18n.locale = sessionStorage.getItem("locale");
      } else {
        sessionStorage.setItem("locale", this.$i18n.locale);
      }
    },
  };
  </script>