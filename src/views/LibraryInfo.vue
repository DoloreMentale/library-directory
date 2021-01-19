<template>
  <v-container class="my-5">
    <v-sheet elevation="2"
             class="pa-5"
             rounded>
      <v-row align="center">
        <v-col class="d-flex flex-column justify-center align-center">
          <h3 class="text-center primary--text mb-3">{{ dbItem.data.general.name }}</h3>
          <v-img :src="dbItem.data.general.image.url"
                 lazy-src="https://picsum.photos/500/500"
                 height="400px"
                 width="400px"/>
          <div class="mt-5">
            <v-divider/>
            <p>{{ dbItem.data.general.address.fullAddress }}</p>
            <p>Сайт библиотеки:
              <a :href="dbItem.data.general.contacts.website">
                {{ dbItem.data.general.contacts.website || 'отсутствует' }}
              </a>
            </p>
            <p>
              Email: {{ dbItem.data.general.contacts.email || 'отсутствует' }}
            </p>
            <v-list>
              <v-list-item-title>Часы работы</v-list-item-title>
              <v-list-item v-for="(value, name, index) in dbItem.data.general.workingSchedule"
                           :key="index">
                {{ name }}: {{ value.from.substring(value.from.lastIndex, 5) }} - {{ value.to.substring(value.to.lastIndex, 5) }}
              </v-list-item>
            </v-list>
            <v-divider/>
          </div>
        </v-col>
        <v-col>
          <h3>Подробнее о библиотеке</h3>
          <div v-html="dbItem.data.general.description"/>
        </v-col>
      </v-row>
    </v-sheet>

  </v-container>
</template>

<script>
import db from '@/db.json'

export default {
  name: "LibraryInfo",
  data() {
    return {
      db
    }
  },
  computed: {
    dbItem() {
      let item
      db.forEach(dbItem => {
        if (dbItem._id === this.$route.params.id) {
          item = dbItem
        }
      })
      return item
    }
  },
}
</script>

<style scoped>

</style>
