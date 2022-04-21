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
        @change="handlerChange"
        @input="handlerInput"
        @keyup.native="handlerKeyupNative"
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
    separator: {
      type: String,
      default: '-',
    },
  },

  computed: {
    // date: {
    //   get (): string | null {
    //     return this.value
    //   },
    //   set (value : string | null) {
    //     console.log('date set', value)
    //     this.$emit('change', value)
    //   }
    // },
  },

  data: () => ({
    date: (new Date(Date.now() - (new Date()).getTimezoneOffset() * 60000)).toISOString().substring(0, 10),
    menu: false,
  }),

  methods: {
    handlerChange (val: string) {
      console.log('changed', val)
    },
    handlerInput (val: string) {
      console.log('inputed', val)
      this.date = this.maskDate(val)
    },
    handlerKeyupNative (val: any) {
      console.log('keyup.native', val)
      console.log('selectionStart', val.target.selectionStart)
    },

    maskDate (value : string): string {
      const v: string = value.replace(/\D/g, '').slice(0, 10)
      const sh = '####-##-##' // 'yyyy-mm-dd'
      const len = sh.split(this.separator).map((x: string): number => x.length)
      let result = '' // sh
      console.log('len', len)
      len.reduce((pv: number, cv: number, index): number => {
        result = result.replace('##', v.slice(pv, pv + cv).padEnd(cv, '_'))
        return pv + cv
      }, 0)
      // result = result
      //   .replace('yyyy', v.slice(0, len[0]).padEnd(len[0], '_'))
      //   .replace('mm', v.slice(len[0], len[0] + len[1]).padEnd(len[1], '_'))
      //   .replace('dd', v.slice(6, 8).padEnd(2, '_'))

      return result
      // if (v.length >= 7) {
      //   return `${v.slice(0, 4)}${this.separator}${v.slice(4, 6)}${this.separator}${v.slice(6)}`
      // } else if (v.length >= 5) {
      //   return `${v.slice(0, 4)}${this.separator}${v.slice(4)}`
      // }
      // return v
    }
  },

})
</script>

<style>

</style>
