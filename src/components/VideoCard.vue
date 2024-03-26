<template>
  <v-card
    class="content-bg card mx-auto"
    :max-width="card.maxWidth"
    flat
    tile
    router
    :to="video.url"
  >
    <v-img :src="video.thumb" height="200px" cover></v-img>
    <v-row no-gutters>
      <v-col cols="auto">
        <v-list-item class="pl-0 pt-3">
          <template v-slot:prepend>
            <v-avatar color="grey darken-3" :image="channel.avatar"> </v-avatar>
          </template>
          <v-list-item-title>{{ video.title }}</v-list-item-title>
          <v-list-item-subtitle>{{ channel.name }}</v-list-item-subtitle>
          <v-list-item-subtitle
            >{{ video.views }} views<v-icon>mdi-circle-small</v-icon
            >{{ video.createdAt }}</v-list-item-subtitle
          >
        </v-list-item>
      </v-col>
    </v-row>
  </v-card>
</template>

<script setup>
defineProps({
  card: Object,
  video: Object,
  channel: Object,
});
</script>
