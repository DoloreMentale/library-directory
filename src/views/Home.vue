<template>
  <v-container class="my-5">
    <v-row>
      <v-col>
        <h1 class="text-center primary--text">Все библиотеки</h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-autocomplete
            v-model="titleValue"
            :items="libraryTitles"
            clearable
            label="Поиск нужной библиотеки"
        ></v-autocomplete>
      </v-col>
    </v-row>
    <v-row justify="center">
      <v-col v-for="(item, index) in db.filter(dbItem => titleValue !== null ? dbItem.data.general.name === titleValue : true)"
             :key="index"
             sm="4">
        <v-card height="100%"
                class="d-flex flex-column">
          <v-img :src="item.data.general.image.url"
                 max-height="250px">
            <template v-slot:placeholder>
              <v-row
                  class="fill-height ma-0"
                  align="center"
                  justify="center">
                <v-progress-circular
                    indeterminate
                    color="light-blue accent-1"
                ></v-progress-circular>
              </v-row>
            </template>
          </v-img>
          <v-card-title id="title">
            {{ item.data.general.name }}
          </v-card-title>
          <v-card-text>{{ item.data.general.address.fullAddress }}</v-card-text>
          <v-spacer/>

          <v-divider/>

          <v-card-text>
            Сайт библиотеки:
            <a :href="item.data.general.contacts.website">{{
                item.data.general.contacts.website || 'отсутствует'
              }}</a>
          </v-card-text>
          <v-card-text>
            Email: {{ item.data.general.contacts.email || 'отсутствует' }}
          </v-card-text>

          <v-divider/>

          <v-btn text
                 @click.prevent="router.push({name: 'LibraryInfo', params: { id: item._id}})">
            Подробнее
          </v-btn>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import db from '@/db.json'
import router from "@/router";

export default {
  name: "Home",
  data() {
    return {
      db: db.slice(0, 100),
      titleValue: null,
      isActive: false,
      router
    }
  },
  computed: {
    libraryTitles: () => {
      let titles = []
      db.forEach(item => titles.push(item.data.general.name))
      return titles
    },
  },
}
</script>

<style scoped>
#title {
  font-size: medium;
}
</style>
