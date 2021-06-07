<template>
  <main>
    <app-nav @showSidebar="state.showSidebar = true" @showWorldbar="state.showWorldbar = true"></app-nav>
    <app-sidebar v-if="state.showSidebar" @close="state.showSidebar = false"></app-sidebar>
    <app-worldbar v-if="state.showWorldbar" @close="state.showWorldbar = false"></app-worldbar>
    <div v-if="state.retrieved" class="flex relative" style="height: calc(100vh - 64px)">
      <chapter-details-panel
        v-if="state.showChapterDetails"
        v-bind="{ activeFile }"
        class="lg:w-2/12 w-full lg:block py-4"
      ></chapter-details-panel>
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
      <world-panel
        v-if="state.showWorldPanel"
        class="lg:w-3/12 w-full lg:block py-4"
      ></world-panel>
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
import AppWorldbar from '~/components/app/AppWorldbar.vue';
import ChapterDetailsPanel from '~/components/app/panels/ChapterDetailsPanel.vue';
import WorldPanel from '~/components/app/panels/WorldPanel.vue';

export default {
  components: { AppNav, AppEditor, AppPreview, AppSidebar, AppWorldbar, ChapterDetailsPanel, WorldPanel },
  setup() {
    const store = useStore();

    const state = shallowReactive({
      retrieved:          false,
      // TODO: These should all be moved into / read from the settings state
      showSidebar:        false,
      showWorldbar:       false,
      showPreview:        false,
      showWorldPanel:     true,
      showChapterDetails: true
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
      activeFile
    };
  },
};
</script>
