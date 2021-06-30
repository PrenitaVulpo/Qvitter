<template>
  <q-page class="q-pa-lg">
    <h4 class="q-mt-none text-weight-bold">About</h4>
    <div class="text-body1">
      <p>
        This little project was created to test the quasar library based on a
        tutorial by freecodecamp on the subject, but I made some small tweaks on
        it.
      </p>

      <p>Where you can find me:</p>

      <a
        v-for="(contact, index) in contacts"
        :key="index"
        class="about-logos q-mb-md"
        :href="`${contact.href}`"
      >
        <img
          class="q-mr-sm"
          width="32"
          height="32"
          :src="`${contact.directory}`"
          alt="{{ contact.alt }}"
        />
        <span>{{ contact.text }}</span>
      </a>
    </div>
  </q-page>
</template>

<script lang="ts">
import { Todo, Meta } from 'components/models';
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'PageIndex',
  components: {},
  setup() {
    const todos = ref<Todo[]>([
      {
        id: 1,
        content: 'ct1',
      },
      {
        id: 2,
        content: 'ct2',
      },
      {
        id: 3,
        content: 'ct3',
      },
      {
        id: 4,
        content: 'ct4',
      },
      {
        id: 5,
        content: 'ct5',
      },
    ]);
    const meta = ref<Meta>({
      totalCount: 1200,
    });

    const contacts = ref([
      {
        directory: 'Images/LI-In-Bug.png',
        alt: 'linkedin',
        text: 'guilherme-damasceno-85480211b/',
        href: 'https://www.linkedin.com/in/guilherme-damasceno-85480211b/',
      },
      {
        directory: 'Images/GitHub-Mark-64px.png',
        alt: 'github',
        text: 'PrenitaVulpo/',
        href: 'https://github.com/PrenitaVulpo',
      },
    ]);
    return { todos, meta, contacts };
  },
});
</script>

<style>
.about-logos {
  display: flex;
  flex-direction: row;
  align-items: center;
  text-decoration: none;
  cursor: pointer;
  color: #000;
  transition: 0.2s;
}
.about-logos:hover {
  background-color: rgb(0, 0, 0, 0.2);
}
</style>
