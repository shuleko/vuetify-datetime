<template>
  <v-app>
    <v-main>

      <DateTime class="ma-8"></DateTime>

    </v-main>
  </v-app>
</template>

<script>
import DateTime from '@/components/DateTime.vue'

export default {
  name: 'App',

  components: {
    DateTime,
  },

  data: () => ({
    //
  })
}
</script>
