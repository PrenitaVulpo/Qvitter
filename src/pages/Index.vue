<template>
  <q-page>
    <div class="q-py-lg q-px-md row items-end q-col-gutter-md">
      <div class="col">
        <q-input
          class="new-qweet"
          filled
          bottom-slots
          v-model="newQweetContent"
          placeholder="What's happening?"
          counter
          autogrow
          maxlength="280"
        >
          <template v-slot:before>
            <q-avatar size="xl">
              <img src="~/assets/Images/user.png" />
            </q-avatar>
          </template>

          <template v-slot:append>
            <q-icon
              v-if="newQweetContent !== ''"
              name="close"
              @click="text = ''"
              class="cursor-pointer"
            />
          </template>

          <!-- <template v-slot:after>

          </template> -->
        </q-input>
      </div>
      <div class="col col-shrink q-mb-md">
        <q-btn
          class="q-py-sm q-px-md text-weight-bold"
          unelevated
          rounded
          color="primary"
          label="Qweet"
          :disable="!newQweetContent"
        />
      </div>
    </div>
    <q-separator size="10px" color="grey-2" class="divider" />
    <q-list>
      <q-item clickable v-ripple>
        <q-item-section avatar top>
          <q-avatar>
            <img src="https://cdn.quasar.dev/img/avatar2.jpg" />
          </q-avatar>
        </q-item-section>

        <q-item-section v-for="qweet in qweetList" :key="qweet">
          <div class="row items-center">
            <q-item-label lines="1" class="col col-shrink text-subtitle1">{{
              qweet.user
            }}</q-item-label>
            <div class="q-mr-xs" />
            <q-item-label
              lines="1"
              class="q-mt-none col col-shrink text-weight-light"
              >{{ qweet.username }}</q-item-label
            >
            <div class="q-mx-xs dot" />
            <q-item-label lines="1" class="q-mt-none col col-shrink">{{
              qweet.time
            }}</q-item-label>
          </div>
          <q-item-label caption class="qweet-content text-body1">
            {{ qweet.content }}
          </q-item-label>
        </q-item-section>
      </q-item>

      <q-separator inset="item" />
    </q-list>
  </q-page>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'PageIndex',
  components: {},
  setup() {
    const newQweetContent = ref('');
    const qweetList = ref([
      {
        user: 'Anna',
        username: '@annamana',
        time: '1 min ago',
        content: `Lorem ipsum dolor, sit amet consectetur adipisicing elit.

      Dolorum
            ipsum quam labore quidem similique velit vitae natus ut consequatur
            ad recusandae, veritatis inventore eligendi quae dolore quas,
            voluptate quaerat exercitationem`,
      },
    ]);

    return { newQweetContent, qweetList };
  },
});
</script>
<style scoped lang="sass">
.new-qweet
  font-size: 1.1875rem
  line-height: 1.4

.divider
  border-top: 1px solid
  border-bottom: 1px solid
  border-color: $grey-4
.qweet-content
  white-space: pre-line
.dot
  background: #9BA4AC
  height: 5px
  width: 5px
  border-radius: 100%
</style>
