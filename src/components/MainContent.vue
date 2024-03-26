<template>
  <v-sheet class="pa-4">
    <v-container fluid>
      <v-row>
        <v-col
          cols="12"
          sm="6"
          md="4"
          lg="3"
          v-for="i in loading ? 10 : 12"
          :key="i"
          class="mx-xs-auto"
        >
          <v-skeleton-loader type="card-avatar" :loading="loading">
            <VideoCard
              v-for="video in videos"
              :card="{ maxWidth: 350 }"
              :video="video"
              :channel="channel"
              class="mb-4"
            ></VideoCard>
          </v-skeleton-loader>
        </v-col>
      </v-row>
    </v-container>
  </v-sheet>
</template>
<script setup lang="ts">
import { ref, onMounted } from "vue";
import VideoCard from "./VideoCard.vue";

const loading = ref(true);

onMounted(() => {
  setTimeout(() => {
    loading.value = false;
  }, 3000);
});

const videos = ref([
  {
    url: "/videos/1",
    thumb: "https://cdn.quasar.dev/img/parallax1.jpg",
    title: "Top 10 places to visit in Uganda",
    views: "1.5M",
    createdAt: "2 weeks ago",
  },

  {
    url: "/watch/13",
    thumb: "https://cdn.quasar.dev/img/mountains.jpg",
    title: "Top 10 places to visit in Asia",
    views: "1.2M",
    createdAt: "1 year ago",
  },
  {
    url: "/watch/14",
    thumb: "https://cdn.quasar.dev/img/quasar.jpg",
    title: "Top 10 places to visit in Europe",
    views: "1.7M",
    createdAt: "a day ago",
  },
  {
    url: "/watch/15",
    thumb: "https://cdn.vuetifyjs.com/images/cards/road.jpg",
    title: "Top 10 places to visit in Africa",
    views: "1.2M",
    createdAt: "1 year ago",
  },
  {
    url: "/watch/16",
    thumb: "https://cdn.vuetifyjs.com/images/cards/plane.jpg",
    title: "Top 10 places to visit in Asia",
    views: "1.2M",
    createdAt: "1 year ago",
  },
  {
    url: "/watch/17",
    thumb: "https://cdn.vuetifyjs.com/images/cards/store.jpg",
    title: "Top 10 places to visit in Europe",
    views: "1.2M",
    createdAt: "2 weeks ago",
  },
  {
    url: "/watch/18",
    thumb: "https://cdn.vuetifyjs.com/images/cards/road.jpg",
    title: "Top 10 places to visit in Africa",
    views: "1.2M",
    createdAt: "2 weeks ago",
  },
  {
    url: "/watch/19",
    thumb: "https://cdn.vuetifyjs.com/images/cards/plane.jpg",
    title: "Top 10 places to visit in Asia",
    views: "1.2M",
    createdAt: "2 weeks ago",
  },
  {
    url: "/watch/20",
    thumb: "https://cdn.vuetifyjs.com/images/cards/store.jpg",
    title: "Top 10 places to visit in Europe",
    views: "1.2M",
    createdAt: "1 year ago",
  },
]);

const channel = ref({
  url: "/channels/12",
  name: "John Doe",
  avatar: "https://randomuser.me/api/portraits/men/4.jpg",
});
</script>
