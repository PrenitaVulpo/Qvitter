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
  </q-page>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

export default defineComponent({
  name: 'PageIndex',
  components: {},
  setup() {
    const newQweetContent = ref('');

    return { newQweetContent };
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
</style>
