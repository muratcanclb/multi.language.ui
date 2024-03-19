<template>
  <div>
    <VCard title="Create Awesome 🙌">
      <VCardText>This is your second page.</VCardText>
      <VCardText>
        Chocolate sesame snaps pie carrot cake pastry pie lollipop muffin.
        Carrot cake dragée chupa chups jujubes. Macaroon liquorice cookie
        wafer tart marzipan bonbon. Gingerbread jelly-o dragée
        chocolate.
      </VCardText>
    </VCard>
    <VCard>
      <select v-model="$i18n.locale">
        <option v-for="locale in $i18n.availableLocales" :key="locale" :value="locale">{{ locale }}</option>
      </select>
      <VCardText>{{ $t("Login") }}</VCardText>
    </VCard>
  </div>
</template>

<script setup lang="ts">
</script>
