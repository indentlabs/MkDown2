<template>
  <nav class="shadow-lg h-16 flex items-center px-5">
    <ui-button icon class="mr-4" @click="$emit('showSidebar', true)">
      <v-mdi name="mdi-book"></v-mdi>
    </ui-button>
    <ui-button icon class="mr-4" @click="$emit('showWorldbar', true)">
      <v-mdi name="mdi-earth"></v-mdi>
    </ui-button>
    <nav-toolbar class="flex-1 mr-6"></nav-toolbar>
    <nav-menu></nav-menu>
  </nav>
</template>
<script>
import NavToolbar from './nav/NavToolbar.vue';
import NavMenu from './nav/NavMenu.vue';

export default {
  components: { NavToolbar, NavMenu },
  emits: ['showSidebar', 'showWorldbar'],
};
</script>
