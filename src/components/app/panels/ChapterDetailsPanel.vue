<template>
  <div
    class="bg-indigo-900 border-l-4 border-indigo-800 px-4 py-3"
  >
    <!-- TODO: previous chapter link
    <div class="flex-1">
      previous chapter
    </div>
    -->
    <div class="flex">
      <div class="py-1 pr-2">
        <v-mdi name="mdi-pencil" size="24"></v-mdi>
      </div>
      <div>
        <p class="font-bold">activeFile.title</p>
        <p class="text-sm scroll">activeFile.description || 'Click here to add an outline'</p>
        <!-- TODO: characters in this scene -->
        <!-- TODO: locations in this scene -->
        <!-- TODO: chapter outline -->
        <!-- TODO: common keyboard controls help/reminder -->
        <!-- TODO: created at / last edited at -->
        <!-- TODO: word count / reader time estimate -->
        <!-- TODO: main idea, themes, symbols, motifs, key facts -->
        <!-- TODO: show previous/next chapter links at bottom/top of sidebar -->
      </div>
    </div>
    <!-- TODO: next chapter link
    <div class="flex-1">
      next chapter
    </div>
    -->
  </div>
</template>
<script>
import { shallowReactive, computed } from 'vue';
import { useStore } from 'vuex';
import { closeAllTooltip } from '~/utils/helper';

export default {
  setup() {
    const store = useStore();

    const state = shallowReactive({ });

    const files = computed(() => store.getters['files/all']);

    return {
      files,
      state
    };
  },
};
</script>
