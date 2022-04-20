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
        :label="label"
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

  model: {
    prop: 'value',
    event: 'change'
  },

  props: {
    value: {
      type: String || null,
      default: null,
    },
    label: {
      type: String || null,
      default: null,
    },
  },

  computed: {
    date: {
      get (): string | null {
        return this.value
      },
      set (value : string | null) {
        console.log('date set', value)
        this.$emit('change', value)
      }
    },
  },

  data: () => ({
    // date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substring(0, 10),
    menu: false,
  }),

})
</script>

<style>

</style>
