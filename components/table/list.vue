<template>
  <div class="col-lg-8">
    <table class="table">
      <thead>
        <tr>
          <td>{{ board }}</td>
          <td>
            <NuxtLink :to="allLink" :class="{ 'red-text': isRedText }">{{ allText }}</NuxtLink>
          </td>
          <td colspan="2">
            <div class="item">
              <NuxtLink v-for="(item, index) in items" :key="index" :to="'#'">{{ item.text }}</NuxtLink>
            </div>
          </td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(category, index) in categories" :key="index">
          <td></td>
          <td :style="{ color: category.color }">{{ category.name }}</td>
          <td colspan="2">
            <div class="item">
              <NuxtLink v-for="(subItem, subIndex) in category.subItems" :key="subIndex" :to="'#'">{{ subItem.text }}
              </NuxtLink>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
  <div class="col-lg-4">
    <table class="table">
      <thead>
        <tr>
          <td colspan="2">
            <div class="item">
              <NuxtLink :class="{ 'category': isCategory }">{{ categoryText }}</NuxtLink>
              <NuxtLink v-for="(link, index) in links" :key="index" :to="'#'" :style="{ color: link.color }">{{
                link.text }}</NuxtLink>
            </div>
          </td>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td colspan="2">
            <div class="item">
              <NuxtLink :class="{ 'category': isCategory }">{{ sortingText }}</NuxtLink>
              <NuxtLink v-for="(sortingLink, index) in sortingLinks" :key="index" :to="'#'"
                :style="{ color: sortingLink.color, 'text-decoration': sortingLink.textDecoration }">{{ sortingLink.text
                }}</NuxtLink>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
    <div class="btn-container">
      <button type="button" class="btn btn-warning custom-btn">{{ publishText }}</button>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

const board = ref('看板');
const allText = ref('全部');
const allLink = ref('#');
const isRedText = ref(true);
const items = ref([
  { text: '閒聊', link: '#' },
  { text: '都蘭特區', link: '#' },
  { text: '過關炫耀', link: '#' },
  { text: '公告', link: '#' }
]);
const categories = ref([
  {
    name: '棒球', color: 'green', subItems: [
      { text: 'MLB', link: '#' },
      { text: '日棒', link: '#' },
      { text: '中職', link: '#' },
      { text: '韓棒', link: '#' },
      { text: '墨棒', link: '#' },
      { text: '澳棒', link: '#' },
      { text: '國際棒賽', link: '#' }
    ]
  },
  {
    name: '籃球', color: 'green', subItems: [
      { text: 'NBA', link: '#' },
      { text: 'WNBA', link: '#' },
      { text: '韓籃', link: '#' },
      { text: '日籃', link: '#' },
      { text: '歐籃', link: '#' },
      { text: '中籃', link: '#' },
      { text: 'P+', link: '#' },
      { text: 'T1', link: '#' },
      { text: '國際籃賽', link: '#' },
      { text: '綜合籃賽', link: '#' },
      { text: '菲籃', link: '#' },
      { text: '澳籃', link: '#' },
    ]
  },
  {
    name: '其他', color: 'green', subItems: [
      { text: '玩競猜', link: '#' },
      { text: '足球', link: '#' },
      { text: 'NHL冰球', link: '#' },
      { text: '俄冰', link: '#' },
      { text: '美足', link: '#' },
      { text: '網球', link: '#' },
      { text: '賽馬', link: '#' },
      { text: '電競', link: '#' },
      { text: '彩球', link: '#' },
      { text: '排球', link: '#' },
      { text: '乒乓球', link: '#' },
      { text: '羽球', link: '#' },
    ]
  },
]);
const categoryText = ref('分類');
const isCategory = ref(true);
const links = ref([
  { text: '全部', href: '#', color: 'red' },
  { text: '分析', href: '#', color: 'black' },
  { text: '感謝', href: '#', color: 'black' },
  { text: 'Live', href: '#', color: 'black' },
  { text: '亮單', href: '#', color: 'black' }
]);
const sortingText = ref('排序');
const sortingLinks = ref([
  { text: '最新回覆', href: '#', color: 'red', textDecoration: 'none' },
  { text: '最新文章', href: '#', color: 'black', textDecoration: 'none' }
]);
const publishText = ref('發表文章');
</script>

<style scoped>
table {
  border-collapse: collapse;
  width: 100%;
  font-family: Arial, sans-serif;
}

td,
th {
  border: none;
  text-align: left;
  padding: 8px;
  font-size: 13px;
}

.red-text {
  color: red;
  text-decoration: none;
}

.red-text:hover {
  text-decoration: underline;
}

.item a {
  margin-right: 14px;
  color: rgb(33, 89, 168);
  text-decoration: none;
}

.item a:hover {
  color: blue;
  text-decoration: underline;
}

.item a.category {
  margin-right: 14px;
  color: black;
  text-decoration: none;
}

.item a.black-text {
  color: black;
}

.underline-on-hover:hover {
  text-decoration: underline;
}

.custom-btn {
  font-size: 15px;
  border-radius: 12px;
  margin-top: 15px;
}

.custom-btn:hover {
  background-color: rgb(254, 130, 5);
}

.btn-container {
  display: flex;
  justify-content: flex-end;
}


@media screen and (max-width: 700px) {
  .item a {
    margin-right: 10px;
  }

  th,
  td {
    padding: 6px;
    font-size: 10px;
  }
}

@media screen and (max-width: 520px) {
  .item a {
    margin-right: 8px;
  }

  th,
  td {
    padding: 4px;
    font-size: 9px;
  }
}
</style>