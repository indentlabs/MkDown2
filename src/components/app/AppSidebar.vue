<template>
  <div
    class="absolute w-full h-full top-0 left-0 z-10 bg-black bg-opacity-25"
    @click="$emit('close')"
  ></div>
  <div
    class="bg-gray-800 w-full lg:w-96 md:w-72 scroll overflow-auto p-5 absolute left-0 h-full top-0 z-20"
  >
    <div class="mb-8 flex items-center">
      <div class="flex-1">
        <p class="text-xl font-bold inline-block">
          Really long book name that will probably wrap, maybe even twice or thrice
        </p>
        <p class="text-gray-300">
          by
          <span class="text-green-500">Your Name</span>
        </p>
      </div>
      <div class="flex flex-col">
        <!-- TODO: switch documents? -->
        <v-mdi name="mdi-close" class="cursor-pointer flex-1" @click="$emit('close')"></v-mdi>
        <div class="flex-1">&nbsp;</div>
        <ui-popover>
          <template #trigger>
            <v-mdi name="mdi-dots-horizontal" class="cursor-pointer"></v-mdi>
          </template>
          <ui-list class="space-y-1">
            <ui-list-item class="cursor-pointer" @click="console.log('clicked edit')">
              <v-mdi name="mdi-pencil" class="mr-4 -ml-1"></v-mdi>
              Edit book title
            </ui-list-item>
          </ui-list>
        </ui-popover>
      </div>
    </div>
    <sidebar-menu class="md:hidden"></sidebar-menu>
    <sidebar-files></sidebar-files>
  </div>
</template>
<script>
import SidebarFiles from './sidebar/SidebarFiles.vue';
import SidebarMenu from './sidebar/SidebarMenu.vue';

export default {
  components: { SidebarFiles, SidebarMenu },
  emits: ['close'],
};
</script>
