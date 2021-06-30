<template>
  <q-layout view="lHr lpR fFf">
    <q-header bordered class="bg-white text-black text-weight-bold">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title> Qwitter </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      :width="283"
      show-if-above
      v-model="leftDrawerOpen"
      side="left"
      bordered
    >
      <q-icon class="q-pa-md" name="fas fa-dove" size="lg" color="primary" />
      <q-list>
        <q-item to="/" clickable v-ripple exact>
          <q-item-section avatar>
            <q-icon name="home" size="md" />
          </q-item-section>

          <q-item-section class="text-h6 text=weight-bold">Home</q-item-section>
        </q-item>
        <q-item to="/about" clickable v-ripple exact>
          <q-item-section avatar>
            <q-icon name="help" size="md" />
          </q-item-section>

          <q-item-section class="text-h6 text=weight-bold"
            >About</q-item-section
          >
        </q-item>
      </q-list>
    </q-drawer>

    <q-drawer show-if-above v-model="rightDrawerOpen" side="right" bordered>
      <q-input
        placeholder="Search Qwitter"
        class="q-ma-md"
        color="teal"
        dense
        rounded
        standout
      >
        <template v-slot:prepend>
          <q-icon name="search" />
        </template>
      </q-input>

      <q-list bordered padding>
        <q-item
          class="q-pa-md"
          v-for="headline in headlinesList"
          :key="headline.labelOverline"
        >
          <q-item-section>
            <q-item-label overline>{{ headline.labelOverline }}</q-item-label>
            <q-item-label>{{ headline.label }}</q-item-label>
            <q-item-label caption>
              {{ headline.caption }}
            </q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const leftDrawerOpen = ref(false);
    const rightDrawerOpen = ref(false);

    const headlinesList = ref([
      {
        labelOverline: 'Sports',
        label: 'Some team defeated some other team!',
        caption:
          'Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit elit',
      },
      {
        labelOverline: 'Games',
        label: 'Brand new title!',
        caption:
          'Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit elit',
      },
      {
        labelOverline: 'Tecnology',
        label: 'Some robot did something!',
        caption:
          'Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit elit',
      },
      {
        labelOverline: 'Science',
        label: 'covid-20 is  now released!',
        caption:
          'Secondary line text. Lorem ipsum dolor sit amet, consectetur adipiscit elit',
      },
    ]);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },

      rightDrawerOpen,
      toggleRightDrawer() {
        rightDrawerOpen.value = !rightDrawerOpen.value;
      },
      headlinesList,
    };
  },
};
</script>
