<template>
  <v-menu
    v-model="menu"
    :close-on-content-click="false"
    :close-on-click = "false"
    :nudge-right="40"
    transition="scale-transition"
    offset-y
    min-width="auto"
  >
    <template #activator="{on}">
      <v-text-field
        v-model="date"
        label="Picker without buttons"
        prepend-inner-icon="mdi-calendar-blank-outline"
        @click:prepend-inner="on.click"
      ></v-text-field>
    </template>
    <v-date-picker
      v-model="date"
      @input="menu = false"
    ></v-date-picker>
  </v-menu>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'DateTime',

  data: () => ({
    date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substring(0, 10),
    menu: false,
  }),

})
</script>

<style>

</style>
