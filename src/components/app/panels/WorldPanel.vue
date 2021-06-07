<template>
  <div
    class="bg-blue-700 border-r-4 border-blue-800 px-4 py-3 scroll"
  >
    <div class="mt-2 mb-3">
      <p class="font-bold mb-2">
        <v-mdi name="mdi-earth" size="32"></v-mdi>
        { active world item }
      </p>
      <p class="text-sm scroll">
        { active world item description }
      </p>

      <p class="mt-4">
        { loop over categories }<br />
          { field / value }
      </p>
    </div>
  </div>
</template>
<script>
import { shallowReactive, computed } from 'vue';
import { useStore } from 'vuex';

export default {
  props: {
    activeFile: {
      type: Object,
      default: () => ({}),
    },
  },
  setup() {
    const store = useStore();
    const state = shallowReactive({ });

    return {
      state
    };
  },
};
</script>
