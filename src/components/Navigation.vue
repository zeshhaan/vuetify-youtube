<template>
  <nav id="navbar">
    <v-app-bar class="white" flat app :order="mobile ? 1 : 0">
      <template v-slot:prepend
        ><v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon
      ></template>
      <v-app-bar-title class="font-weight-bold text-h6 toolbar-container">
        <Icon width="30" icon="logos:youtube-icon" />
        <span class="ml-2">YouTube</span>
      </v-app-bar-title>
      <v-spacer></v-spacer>
      <v-text-field
        v-if="!mobile"
        variant="outlined"
        flat
        hide-details
        single-line
        append-inner-icon="mdi-magnify"
        label="Search"
        density="compact"
        v-model="searchText"
        @click:append="search"
        class="search-bar"
      >
        <template v-slot:append>
          <v-btn
            density="default"
            variant="tonal"
            icon="mdi-microphone"
          ></v-btn>
        </template>
      </v-text-field>

      <v-spacer v-if="!mobile"></v-spacer>
      <v-menu offsetY v-if="!mobile">
        <template v-slot:activator="{ props: menu }">
          <v-tooltip location="bottom">
            <template v-slot:activator="{ props: tooltip }">
              <v-btn icon v-bind="{ ...tooltip, ...menu }" class="mr-3"
                ><v-icon size="25">mdi-dots-vertical</v-icon></v-btn
              >
            </template>
            <span>Create a video and more</span>
          </v-tooltip>
        </template>
        <v-list>
          <v-list-item v-for="(item, index) in options" :key="index">
            <template v-slot:prepend>
              <v-icon :icon="item.icon"></v-icon>
            </template>
            <v-list-item-title v-text="item.title"></v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
      <v-menu offset-y left>
        <template v-slot:activator="{ props }">
          <v-btn
            v-if="mobile"
            v-bind="props"
            color="blue"
            size="large"
            density="compact"
            icon="mdi-account"
            rounded="xl"
            variant="outlined"
          >
          </v-btn>
          <v-btn
            v-else
            v-bind="props"
            color="blue"
            size="large"
            density="comfortable"
            prepend-icon="mdi-account"
            rounded="xl"
            variant="outlined"
          >
            约翰·多伊</v-btn
          >
        </template>

        <v-card>
          <v-list>
            <v-list-item
              prepend-avatar="https://randomuser.me/api/portraits/men/4.jpg"
              subtitle="john@doe.com"
              title="约翰·多伊"
            >
            </v-list-item>
          </v-list>

          <v-divider></v-divider>

          <v-list density="compact">
            <v-list-item
              v-for="(item, index) in profile"
              :key="index"
              :value="item"
            >
              <template v-slot:prepend>
                <v-icon :icon="item.icon"></v-icon>
              </template>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item>
          </v-list>
        </v-card>
      </v-menu>
      <v-tooltip location="bottom" v-if="!mobile">
        <template v-slot:activator="{ props }">
          <v-btn @click="toggleTheme" icon v-bind="props" class="ml-3">
            <Icon width="20" icon="ri:contrast-drop-fill" />
          </v-btn>
        </template>
        <span>Switch theme</span>
      </v-tooltip>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" app id="nav">
      <div tag="div" class="v-navigation-drawer__content">
        <v-list dense nav class="py-0" tag="div">
          <v-list-item v-if="mobile">
            <div class="d-flex align-center">
              <v-app-bar-nav-icon
                @click="drawer = !drawer"
                class="mr-5"
              ></v-app-bar-nav-icon>
              <v-toolbar-title class="font-weight-bold toolbar-container">
                <Icon width="30" icon="logos:youtube-icon" />
                <span class="ml-2">YouTube</span></v-toolbar-title
              >
            </div>
          </v-list-item>
          <v-divider v-if="mobile"></v-divider>
          <v-list density="compact">
            <v-list-item
              v-for="(item, index) in items"
              :key="index"
              :value="item"
            >
              <template v-slot:prepend>
                <v-icon :icon="item.icon"></v-icon>
              </template>
              <v-list-item-title v-text="item.title"></v-list-item-title>
            </v-list-item>
          </v-list>
        </v-list>
      </div>
    </v-navigation-drawer>
    <slot name="main-content" />
  </nav>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import { useDisplay, useTheme } from "vuetify";
import { Icon } from "@iconify/vue";
import VideoCard from "./VideoCard.vue";

const drawer = ref(false);
const loading = ref(false);
const searchText = ref("");

const theme = useTheme();
const { mobile } = useDisplay();
drawer.value = mobile.value;

const search = () => {
  console.log(searchText.value);
};

onMounted(() => {
  setTimeout(() => {
    loading.value = false;
  }, 3000);
});

const toggleTheme = () => {
  theme.global.name.value = theme.global.current.value.dark ? "light" : "dark";
};

const items = ref([
  { title: "Home", link: "/", icon: "mdi-home" },
  { title: "Trending", link: "/trending", icon: "mdi-fire" },
  {
    title: "Your videos",
    link: "/channels/ddd",
    icon: "mdi-play-box-outline",
  },
  {
    title: "Library",
    link: "#l",
    icon: "mdi-play-box-multiple",
  },
  {
    title: "History",
    link: "/history",
    icon: "mdi-history",
  },
]);

const profile = ref([
  {
    title: "Your channel",
    icon: "mdi-account-box",
  },
  {
    title: "YouTube Studio",
    icon: "mdi-youtube-studio",
  },
  {
    title: "Sign out",
    icon: "mdi-login-variant",
  },
]);

const options = ref([
  { title: "Upload video", icon: "mdi-play-box-outline" },
  { title: "Go live", icon: "mdi-access-point" },
]);

// page content
const video = ref({
  url: "/watch/12",
  thumb: "https://cdn.vuetifyjs.com/images/cards/sunshine.jpg",
  title: "Top western road trips",
  views: "9.6k",
  createdAt: "6 hours ago",
});

const channel = ref({
  url: "/channels/12",
  name: "John Doe",
  avatar: "https://randomuser.me/api/portraits/men/4.jpg",
});
</script>

<style lang="scss">
.search-bar .v-field {
  border-radius: 25px !important;
  width: 400px;
}

.search-bar .v-field__outline__start {
  flex: 0 0 25px !important;
  border-top-left-radius: 25px !important;
  border-bottom-left-radius: 25px !important;
}

.toolbar-container .v-toolbar-title__placeholder {
  display: flex;
  align-items: center;
}
</style>
