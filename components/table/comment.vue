<template>
  <div>
    <table class="table table-bordered">
      <thead>
        <tr>
          <td class="title-text" style="padding: 12px" width="584" height="50">
            {{ Title }}
          </td>
          <td class="title-text" style="padding: 12px" width="41"></td>
          <td class="title-text" style="padding: 12px" width="120">
            {{ Authorname }}
          </td>
          <td class="title-text" style="padding: 12px" width="120">
            {{ Newreply }}
          </td>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) in paginatedData" :key="index">
          <td class="center-text" height="55">
            <NuxtLink :to="item.link">{{ item.topic }}</NuxtLink>
          </td>
          <td class="center-text" height="55">
            <NuxtLink :to="item.imagelink">
              <img :src="item.image" alt="thumbnail" width="35" height="35" />
            </NuxtLink>
          </td>
          <td class="center-text author-info" style="text-align: center">
            <NuxtLink :to="item.author.link">
              {{ item.author.name }}<br /><span class="dataitem">{{ item.author.date }}</span>
            </NuxtLink>
          </td>
          <td class="center-text reply-info" style="text-align: center">
            <NuxtLink :to="item.latestReply.link">
              {{ item.latestReply.author }}<br /><span class="dataitem">{{ item.latestReply.date }}</span>
            </NuxtLink>
          </td>
        </tr>
      </tbody>
    </table>

    <div class="pagination">
      <nav aria-label="Page navigation example">
        <ul class="pagination">
          <li class="page-item" :class="{ disabled: currentPage === 1 }">
            <a class="page-link" href="#" aria-label="Previous" @click="prevPage">
              <span aria-hidden="true">&laquo;</span>
            </a>
          </li>
          <li class="page-item" v-for="page in totalPages" :key="page" :class="{ active: page === currentPage }">
            <a class="page-link" href="#" @click="changePage(page)">{{ page }}</a>
          </li>
          <li class="page-item" :class="{ disabled: currentPage === totalPages }">
            <a class="page-link" href="#" aria-label="Next" @click="nextPage">
              <span aria-hidden="true">&raquo;</span>
            </a>
          </li>
        </ul>
      </nav>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref, computed } from "vue";

interface TableDataItem {
  topic: string;
  link: string;
  image: string;
  imagelink: string;
  author: {
    name: string;
    link: string;
    date: string;
  };
  latestReply: {
    author: string;
    link: string;
    date: string;
  };
}

export default defineComponent({
  props: {
    tableData: {
      type: Array as () => TableDataItem[],
      required: true,
    },
    Title: {
      type: String,
      default: "主題",
    },
    Authorname: {
      type: String,
      default: "作者",
    },
    Newreply: {
      type: String,
      default: "最新回覆",
    },
  },
  setup(props) {
    const currentPage = ref(1);
    const itemsPerPage = 10;

    const totalPages = computed(() =>
      Math.ceil(props.tableData.length / itemsPerPage)
    );

    const paginatedData = computed(() => {
      const startIndex = (currentPage.value - 1) * itemsPerPage;
      const endIndex = startIndex + itemsPerPage;
      return props.tableData.slice(startIndex, endIndex);
    });

    const changePage = (page: number) => {
      if (page >= 1 && page <= totalPages.value) {
        currentPage.value = page;
      }
    };

    const nextPage = () => {
      if (currentPage.value < totalPages.value) {
        currentPage.value++;
      }
    };

    const prevPage = () => {
      if (currentPage.value > 1) {
        currentPage.value--;
      }
    };

    return {
      currentPage,
      totalPages,
      paginatedData,
      changePage,
      nextPage,
      prevPage,
    };
  },
});
</script>

<style scoped>
.title-text {
  text-align: center;
}

.center-text {
  text-align: left;
  font-size: 16px;
}

.table-bordered thead tr td {
  background-color: rgb(47, 187, 243);
}

.table-bordered tbody tr:nth-child(even) td {
  background-color: #f6f4f4;
}

.table-bordered tbody tr:nth-child(odd) td {
  background-color: #fff;
}

.table-bordered td {
  padding: 18px;
}

.center-text a {
  color: rgb(33, 89, 168);
  text-decoration: none;
}

.center-text a:hover {
  text-decoration: underline;
  color: blue;
}

.author-info a,
.reply-info a {
  font-size: 12px;
  color: black;
}

.dataitem {
  font-size: 12px;
  color: gray;
}

.author-info a:hover,
.reply-info a:hover,
.dataitem:hover {
  text-decoration: underline;
  color: black;
}

.pagination {
  padding: 15px;
  display: flex;
  justify-content: center;
}

@media (max-width: 768px) {

  .table-bordered td,
  .table-bordered th {
    padding: 8px;
    font-size: 10px;
  }

  .author-info a,
  .reply-info a {
    font-size: 10px;
  }

  .dataitem {
    font-size: 10px;
  }
}
</style>