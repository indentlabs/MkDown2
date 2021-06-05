<template>
  <main>
    <app-nav @showSidebar="state.showSidebar = true"></app-nav>
    <app-sidebar v-if="state.showSidebar" @close="state.showSidebar = false"></app-sidebar>
    <!-- TODO: add world sidebar here / ctrl+f showWorldSidebar -->
    <div v-if="state.retrieved" class="flex relative" style="height: calc(100vh - 64px)">

      <!-- TODO: component-ize this and give it a state.showChapterMeta condition -->
      <div
        class="bg-indigo-900 border-l-4 border-indigo-800 px-4 py-3 lg:w-2/12"
      >
        <div class="flex">
          <div class="py-1 pr-2">
            <v-mdi name="mdi-pencil" size="24"></v-mdi>
          </div>
          <div>
            <p class="font-bold">{{ activeFile.title }}</p>
            <p class="text-sm scroll">{{ activeFile.description || 'Click here to add an outline' }}</p>
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
      </div>

      <app-editor
        v-bind="{ activeFile }"
        class="lg:w-7/12 w-full lg:block bg-black bg-opacity-10 py-4"
        :class="{ hidden: state.showPreview }"
      ></app-editor>
      <app-preview
        v-bind="{ file: activeFile }"
        class="lg:w-5/12 w-full py-4 px-5 overflow-auto scroll lg:block"
        :class="{ hidden: !state.showPreview }"
      ></app-preview>
      <!-- TODO: add more columns/sidebars here -->
      <ui-button
        icon
        variant="primary"
        class="shadow-lg lg:hidden bottom-0 right-0 m-5 z-10"
        style="position: absolute"
        @click="state.showPreview = !state.showPreview"
      >
        <v-mdi :name="state.showPreview ? 'mdi-close' : 'mdi-eye'"></v-mdi>
      </ui-button>
    </div>
  </main>
</template>
<script>
import { computed, shallowReactive, onMounted } from 'vue';
import { useStore } from 'vuex';
import syncScroll from '~/utils/syncScroll';
import AppNav from '~/components/app/AppNav.vue';
import AppEditor from '~/components/app/AppEditor.vue';
import AppPreview from '~/components/app/AppPreview.vue';
import AppSidebar from '~/components/app/AppSidebar.vue';

export default {
  components: { AppNav, AppEditor, AppPreview, AppSidebar },
  setup() {
    const store = useStore();

    const state = shallowReactive({
      retrieved: false,
      showSidebar: false,
      showPreview: false,
    });

    const activeFile = computed(() => store.getters['files/active']);

    store.dispatch('retrieve').then(() => {
      state.retrieved = true;
    });

    onMounted(() => {
      setTimeout(() => {
        syncScroll(['.CodeMirror-scroll', '.preview-container']);
      }, 2000);
    });

    return {
      state,
      activeFile,
    };
  },
};
</script>
