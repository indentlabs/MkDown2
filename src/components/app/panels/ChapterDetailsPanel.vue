<template>
  <div
    class="bg-indigo-900 border-l-4 border-indigo-800 px-4 py-3 scroll"
  >
    <!-- TODO: previous chapter link
    <div class="flex-1">
      previous chapter
    </div>
    -->
    <div class="mt-2 mb-3">
      <p class="font-bold mb-2">
        <v-mdi name="mdi-pencil" size="32"></v-mdi>
        {{ activeFile.title }}
      </p>
      <p class="text-sm scroll">{{ activeFile.description }}</p>
      <!-- TODO: characters in this scene -->
      <!-- TODO: locations in this scene -->
      <!-- TODO: chapter outline -->
      <!-- TODO: common keyboard controls help/reminder -->
      <!-- TODO: created at / last edited at -->
      <!-- TODO: word count / reader time estimate -->
      <!-- TODO: main idea, themes, symbols, motifs, key facts -->
      <!-- TODO: show previous/next chapter links at bottom/top of sidebar -->
    </div>
    <div class="text-gray-400 my-2">
      0 words
    </div>
    <div class="my-3">
      Characters
      <div class="flex -space-x-2 p-2 overflow-hidden">
        <img class="inline-block h-10 w-10 rounded-full ring-2 ring-white" src="https://images.unsplash.com/photo-1491528323818-fdd1faba62cc?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80" alt="">
        <img class="inline-block h-10 w-10 rounded-full ring-2 ring-white" src="https://images.unsplash.com/photo-1550525811-e5869dd03032?ixlib=rb-1.2.1&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80" alt="">
        <img class="inline-block h-8 w-8 rounded-full ring-2 ring-white" src="https://images.unsplash.com/photo-1500648767791-00dcc994a43e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2.25&w=256&h=256&q=80" alt="">
        <img class="inline-block h-8 w-8 rounded-full ring-2 ring-white" src="https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80" alt="">
        <img class="inline-block h-8 w-8 rounded-full ring-2 ring-white" src="https://images.unsplash.com/photo-1500648767791-00dcc994a43e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2.25&w=256&h=256&q=80" alt="">
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
