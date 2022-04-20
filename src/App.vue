<template>
  <v-app>
    <v-main>

      <DateTime
        class="ma-8"
        label="Заголовок"
        v-model="date"
      ></DateTime>

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
    date: '1974-09-01',
  })
}
</script>
