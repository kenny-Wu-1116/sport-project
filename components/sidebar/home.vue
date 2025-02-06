<template>
  <div v-for="(item, index) in sidebarItems" :key="index" class="sidebar">
    <NuxtLink :to="item.link" class="sidebar-link">
      <p>{{ item.text }}</p>
      <span>{{ item.name }}</span>
    </NuxtLink>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

interface SidebarItem {
  name: string;
  text: string;
  link: string;
}

export default defineComponent({
  props: {
    sidebarItems: {
      type: Array as () => SidebarItem[],
      required: true
    }
  }
});
</script>

<style scoped>
.sidebar-link {
  display: block;
}

.sidebar {
  background-color: #faf9f9;
  padding: 12px;
  border-radius: 10px;
  border: 2px solid #eeeaea;
  font-size: 15px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.sidebar:hover {
  transform: scale(1.05);
  box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.2);
  cursor: pointer;
  background-color: #ffffff;
  color: blue;
  text-decoration: underline;
}

.sidebar a {
  color: rgb(33, 89, 168);
  text-decoration: none;
}

@media screen and (max-width: 768px) {
  .sidebar {
    font-size: 13px;
    padding: 10px;
  }
}

@media screen and (max-width: 576px) {
  .sidebar {
    font-size: 10px;
    padding: 6px;
  }
}
</style>
