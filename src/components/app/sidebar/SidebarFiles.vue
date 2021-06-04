<template>
  <div class="mt-4 lg:mt-0">
    <div class="flex items-center mb-4">
      <p class="text-gray-200 flex-1">Outline</p>
      <ui-button icon class="text-primary" @click="addFile">
        <v-mdi name="mdi-plus" size="20"></v-mdi>
      </ui-button>
    </div>
    <ui-list class="space-y-1">
      <ui-list-item
        v-for="file in files"
        :key="file.id"
        :active="file.id === $store.state.files.activeFile"
        class="cursor-pointer"
        @click="changeActive(file.id)"
      >
        <div class="py-1 flex-1 pr-4">
          <p class="text-overflow">
            {{ file.title }}
            <!-- TODO: long titles overflow and menu gets covered up -->
          </p>
          <p class="text-gray-200">
            {{ file.description }}
          </p>
          <p class="text-gray-400">
            {{ file.word_count || 0 }} word{{ file.word_count === 1 ? '' : 's'}}
          </p>
        </div>
        <ui-popover>
          <template #trigger>
            <v-mdi name="mdi-dots-horizontal" class="cursor-pointer"></v-mdi>
          </template>
          <ui-list class="space-y-1">
            <ui-list-item class="cursor-pointer" @click="editFile(file.id, file)">
              <v-mdi name="mdi-pencil" class="mr-4 -ml-1"></v-mdi>
              Edit title & description
            </ui-list-item>
            <ui-list-item
              v-if="files.length !== 1"
              class="text-red-400 cursor-pointer"
              @click="deleteFile"
            >
              <v-mdi name="mdi-delete" class="mr-4 -ml-1"></v-mdi>
              Delete
            </ui-list-item>
          </ui-list>
        </ui-popover>
      </ui-list-item>
    </ui-list>
    <ui-modal v-model="state.showRenameModal" content-class="max-w-sm">
      <template #header>
        <p>Edit title & description</p>
      </template>
      <input
        id="name"
        v-model="state.tempTitle"
        class="rounded-xl bg-gray-100 bg-opacity-5 border-opacity-10 transition focus:ring focus:ring-opacity-50 py-2 px-4 transition w-full"
      />
      <input
        id="description"
        v-model="state.tempDescription"
        class="rounded-xl bg-gray-100 bg-opacity-5 border-opacity-10 transition focus:ring focus:ring-opacity-50 py-2 px-4 transition w-full"
      />
      <div class="flex items-center space-x-2 mt-8">
        <ui-button class="w-6/12" @click="state.showRenameModal = false">
          Cancel
        </ui-button>
        <ui-button variant="primary" class="w-6/12" @click="renameFile">
          Save changes
        </ui-button>
      </div>
    </ui-modal>
  </div>
</template>
<script>
import { shallowReactive, computed } from 'vue';
import { useStore } from 'vuex';
import { closeAllTooltip } from '~/utils/helper';

export default {
  setup() {
    const store = useStore();

    const state = shallowReactive({
      editId: '',
      tempTitle: '',
      tempDescription: '',
      showRenameModal: false,
    });

    const files = computed(() => store.getters['files/all']);

    function addFile() {
      store.dispatch('files/add', {
        activate: true,
        data: {
          title: 'Untitled document',
          description: '',
          content: "Write as little or as much as you'd like!",
        },
      });
    }
    function changeActive(id) {
      store.commit('files/changeActive', id);
    }
    function editFile(id, { title, description }) {
      closeAllTooltip();
      state.editId = id;
      state.tempTitle = title;
      state.tempDescription = description;
      state.showRenameModal = true;
    }
    function renameFile() {
      store.commit('files/updateFile', {
        id: state.editId,
        key: 'title',
        value: state.tempTitle || 'Untitled document'
      });
      store.commit('files/updateFile', {
        id: state.editId,
        key: 'description',
        value: state.tempDescription || ''
      });

      state.showRenameModal = false;
      state.editId = '';
      state.tempTitle = '';
      state.tempDescription = '';
    }
    function deleteFile() {
      store.dispatch('files/delete');
      closeAllTooltip();
    }

    return {
      files,
      state,
      addFile,
      editFile,
      deleteFile,
      renameFile,
      changeActive,
    };
  },
};
</script>
