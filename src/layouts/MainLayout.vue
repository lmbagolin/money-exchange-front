<template>
  <q-layout view="hHh lpR fFf" class="bg-grey-1">
    <q-header elevated class="bg-white text-grey-8" height-hint="64">
      <q-toolbar class="GNL__toolbar">
        <q-btn
          flat
          dense
          round
          @click="toggleLeftDrawer"
          aria-label="Menu"
          icon="menu"
          class="q-mr-sm"
        />

        <q-toolbar-title
          v-if="$q.screen.gt.xs"
          shrink
          class="row items-center no-wrap"
        >
          <img
            src="https://cdn.quasar.dev/img/layout-gallery/logo-google.svg"
          />
          <span class="q-ml-sm">News</span>
        </q-toolbar-title>

        <q-space />

        <q-input
          class="GNL__toolbar-input"
          outlined
          dense
          v-model="search"
          color="bg-grey-7 "
          placeholder="Search for topics, locations & sources"
        />

        <q-space />

        <div class="q-gutter-sm row items-center no-wrap">
          <q-btn round flat>
            <q-avatar size="26px">
              <img src="https://cdn.quasar.dev/img/boy-avatar.png" />
            </q-avatar>
            <q-tooltip>Account</q-tooltip>
          </q-btn>
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      class="bg-white"
      :width="280"
    >
      <q-scroll-area class="fit">
        <q-list padding class="text-grey-8">
          <q-item
            class="GNL__drawer-item"
            v-ripple
            v-for="link in links1"
            :key="link.text"
            clickable
          >
            <q-item-section avatar>
              <q-icon :name="link.icon" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ link.text }}</q-item-label>
            </q-item-section>
          </q-item>

          <q-separator inset class="q-my-sm" />

          <q-item
            class="GNL__drawer-item"
            v-ripple
            v-for="link in links2"
            :key="link.text"
            clickable
          >
            <q-item-section avatar>
              <q-icon :name="link.icon" />
            </q-item-section>
            <q-item-section>
              <q-item-label>{{ link.text }}</q-item-label>
            </q-item-section>
          </q-item>

          <q-separator inset class="q-my-sm" />

          <q-item
            class="GNL__drawer-item"
            v-ripple
            v-for="link in links3"
            :key="link.text"
            clickable
          >
            <q-item-section>
              <q-item-label
                >{{ link.text }} <q-icon v-if="link.icon" :name="link.icon"
              /></q-item-label>
            </q-item-section>
          </q-item>

          <div class="q-mt-md">
            <div class="flex flex-center q-gutter-xs">
              <a
                class="GNL__drawer-footer-link"
                href="javascript:void(0)"
                aria-label="Privacy"
                >Privacy</a
              >
              <span> · </span>
              <a
                class="GNL__drawer-footer-link"
                href="javascript:void(0)"
                aria-label="Terms"
                >Terms</a
              >
              <span> · </span>
              <a
                class="GNL__drawer-footer-link"
                href="javascript:void(0)"
                aria-label="About"
                >About Google</a
              >
            </div>
          </div>
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script setup>
import { ref } from "vue";
import { fasEarthAmericas, fasFlask } from "@quasar/extras/fontawesome-v6";

const leftDrawerOpen = ref(false);
const search = ref("");
const exactPhrase = ref("");
const hasWords = ref("");
const excludeWords = ref("");
const byWebsite = ref("");
const byDate = ref("Any time");

function onClear() {
  exactPhrase.value = "";
  hasWords.value = "";
  excludeWords.value = "";
  byWebsite.value = "";
  byDate.value = "Any time";
}

function toggleLeftDrawer() {
  leftDrawerOpen.value = !leftDrawerOpen.value;
}

const links1 = [
  { icon: "web", text: "Top stories" },
  { icon: "person", text: "For you" },
  { icon: "star_border", text: "Favourites" },
  { icon: "search", text: "Saved searches" },
];
const links2 = [
  { icon: "flag", text: "Canada" },
  { icon: fasEarthAmericas, text: "World" },
  { icon: "place", text: "Local" },
  { icon: "domain", text: "Business" },
  { icon: "memory", text: "Technology" },
  { icon: "local_movies", text: "Entertainment" },
  { icon: "directions_bike", text: "Sports" },
  { icon: fasFlask, text: "Science" },
  { icon: "fitness_center", text: "Health " },
];
const links3 = [
  { icon: "", text: "Language & region" },
  { icon: "", text: "Settings" },
  { icon: "open_in_new", text: "Get the Android app" },
  { icon: "open_in_new", text: "Get the iOS app" },
  { icon: "", text: "Send feedback" },
  { icon: "open_in_new", text: "Help" },
];
</script>

<style lang="scss">
.GNL {
  &__toolbar {
    height: 64px;
  }

  &__toolbar-input {
    width: 55%;
  }

  &__drawer-item {
    line-height: 24px;
    border-radius: 0 24px 24px 0;
    margin-right: 12px;

    .q-item__section--avatar {
      .q-icon {
        color: #5f6368;
      }
    }

    .q-item__label {
      color: #3c4043;
      letter-spacing: 0.01785714em;
      font-size: 0.875rem;
      font-weight: 500;
      line-height: 1.25rem;
    }
  }

  &__drawer-footer-link {
    color: inherit;
    text-decoration: none;
    font-weight: 500;
    font-size: 0.75rem;

    &:hover {
      color: #000;
    }
  }
}
</style>
