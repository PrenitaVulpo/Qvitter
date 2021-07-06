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
              @click="newQweetContent = ''"
              class="cursor-pointer"
            />
          </template>

          <!-- <template v-slot:after>

          </template> -->
        </q-input>
      </div>
      <div class="col col-shrink q-mb-md">
        <q-btn
          @click="addNewQweet"
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
    <transition-group
      appear
      enter-active-class="animated fadeIn"
      leave-active-class="animated fadeOut"
    >
      <q-list v-for="(qweet, index) in qweetList" :key="qweet">
        <q-item clickable v-ripple>
          <q-item-section avatar top>
            <q-avatar>
              <img src="https://cdn.quasar.dev/img/avatar2.jpg" />
            </q-avatar>
          </q-item-section>

          <q-item-section>
            <div class="row items-center q-mb-xs">
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
              <q-item-label
                lines="1"
                class="q-mt-none col col-shrink text-weight-light"
                >{{ relativeDate(qweet.time) }}</q-item-label
              >
            </div>
            <q-item-label caption class="qweet-content text-body1">
              {{ qweet.content }}
            </q-item-label>
            <div
              class="row justify-between q-mt-sm q-pr-xl q-mr-lg qweet-icons"
            >
              <q-btn color="grey" icon="far fa-comment" size="sm" flat round />
              <q-btn color="grey" icon="fas fa-retweet" size="sm" flat round />
              <q-btn color="grey" icon="far fa-heart" size="sm" flat round />
              <q-btn
                v-show="qweet.username !== '@semArroba'"
                color="grey"
                icon="fas fa-share-square"
                size="sm"
                flat
                round
              />
              <q-btn
                @click="deleteQweet(index)"
                v-show="qweet.username === '@semArroba'"
                color="grey"
                icon="fas fa-trash-alt"
                size="sm"
                flat
                round
              />
            </div>
          </q-item-section>
        </q-item>

        <q-separator inset="item" />
      </q-list>
    </transition-group>
  </q-page>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import { formatDistanceToNow } from 'date-fns';
import Qweet from '../TS/Interfaces/Qweet';

export default defineComponent({
  name: 'PageIndex',
  components: {},
  setup() {
    const newQweetContent = ref('');
    const qweetList = ref<Qweet[]>([
      {
        user: 'Anna',
        username: '@annamana',
        time: 1625507373011,
        content: `Lorem ipsum dolor, sit amet consectetur adipisicing elit.

      Dolorum
            ipsum quam labore quidem similique velit vitae natus ut consequaturad recusandae, veritatis inventore eligendi quae dolore quas, voluptate quaerat exercitationem`,
      },
      {
        user: 'Anna',
        username: '@annamana',
        time: 1625507386203,
        content: `Lorem ipsum dolor, sit amet consectetur adipisicing elit.

      Dolorum
            ipsum quam labore quidem similique velit vitae natus ut consequaturad recusandae, veritatis inventore eligendi quae dolore quas, voluptate quaerat exercitationem`,
      },
    ]);

    return { newQweetContent, qweetList };
  },
  methods: {
    addNewQweet() {
      const content = this.newQweetContent;
      if (content) {
        this.qweetList.unshift({
          user: 'Testador',
          username: '@semArroba',
          time: Date.now(),
          content,
        });
      }
      this.newQweetContent = '';
    },
    deleteQweet(index: number) {
      this.qweetList.splice(index, 1);
    },
    relativeDate(time: number) {
      return formatDistanceToNow(time);
    },
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
.qweet-icons
  margin-left: -.5rem
</style>
