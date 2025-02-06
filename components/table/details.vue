<template>
  <table class="table table-bordered">
    <tbody v-for="(item, index) in slicedData" :key="index">
      <tr>
        <td :rowspan="index === 0 ? 2 : 1" width="135" :class="{
          tableleftone:
            (index === 0 && currentPage === 1) ||
            (currentPage > 1 && index === 20),
          tableleft:
            (index !== 0 || currentPage !== 1) &&
            !(currentPage > 1 && index === 20),
          highlight: currentPage > 1 && index === 20,
        }">
          <div v-if="index === 0 && currentPage !== 1" align="center">
            {{ startFloor }}{{ floor }}
          </div>
          <div v-else-if="index > 0" align="center">
            {{ (currentPage - 1) * itemsPerPage + index + 1 }}{{ floor }}
          </div>
          <div class="player">
            <img :src="item.image" width="100" height="100" />
          </div>
          <div class="nickname">
            <a href="#">{{ item.player }}</a>
          </div>
          <div class="level"><i class="bi bi-star"></i>{{ item.level }}</div>
          <div class="lefticon" v-if="index === 0 && currentPage === 1">
            <div class="btn btn-secondary">
              <i class="bi bi-tags"></i>{{ buttontext }}
            </div>
            <div class="peoples">
              <a>{{ item.followers }}</a><span>{{ followertext }}</span>
            </div>
          </div>
        </td>
        <td width="85%" valign="top" :class="{
          tablerightone:
            (index === 0 && currentPage === 1) ||
            (currentPage > 1 && index === 20),
          tableright:
            (index !== 0 || currentPage !== 1) &&
            !(currentPage > 1 && index === 20),
        }">
          <table width="100%" border="0">
            <tbody>
              <tr>
                <td colspan="2" class="date">
                  <div class="options">
                    <span>[<a href="#" @click="goToLatest">到最新回文</a>]</span>
                    <br />
                    <span>{{ item.date }}</span>
                  </div>
                </td>
              </tr>
              <tr>
                <td class="tdcontent" v-html="applyStyles(item.content)"></td>
              </tr>
            </tbody>
          </table>
        </td>
      </tr>
    </tbody>
  </table>

  <div class="downbox">
    <div class="returnbutton">
      <NuxtLink to="/forum">
        <button type="button" class="btn btn-light btn-custom">
          回NBA討論區
        </button>
      </NuxtLink>
    </div>
    <div class="pagination">
      <nav aria-label="Page navigation example">
        <ul class="pagination">
          <li class="page-item" :class="{ disabled: currentPage === 1 }">
            <a class="page-link" href="#" @click.prevent="
              currentPage = currentPage - 1;
            scrollToTop();
            " aria-label="Previous">
              <span aria-hidden="true">&laquo;</span>
            </a>
          </li>
          <li class="page-item" v-for="page in totalPages" :key="page" :class="{ active: currentPage === page }">
            <a class="page-link" href="#" @click.prevent="
              currentPage = page;
            scrollToTop();
            ">{{ page }}</a>
          </li>
          <li class="page-item" :class="{ disabled: currentPage === totalPages }">
            <a class="page-link" href="#" @click.prevent="
              currentPage = currentPage + 1;
            scrollToTop();
            " aria-label="Next">
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

interface TableData {
  player: string;
  level: string;
  content: string;
  date: string;
  image: string;
  followers?: string;
}

export default defineComponent({
  props: {
    data: {
      type: Array as PropType<TableData[]>,
      required: true,
    },
    itemsPerPage: {
      type: Number,
      default: 10,
    },
    buttontext: {
      type: String,
      default: "追蹤發文",
    },
    followertext: {
      type: String,
      default: "人追蹤",
    },
    floor: {
      type: String,
      default: "樓",
    },
  },
  setup(props) {
    const currentPage = ref(1);

    const totalPages = computed(() =>
      Math.ceil(props.data.length / props.itemsPerPage)
    );

    const startIndex = computed(
      () => (currentPage.value - 1) * props.itemsPerPage
    );
    const endIndex = computed(() =>
      Math.min(startIndex.value + props.itemsPerPage, props.data.length)
    );

    const startFloor = computed(
      () => (currentPage.value - 1) * props.itemsPerPage + 1
    );

    const slicedData = computed(() =>
      props.data.slice(startIndex.value, endIndex.value)
    );

    const scrollToTop = () => {
      window.scrollTo(0, 0);
      history.pushState({ page: currentPage.value }, "");
    };

    const goToLatest = () => {
      currentPage.value = totalPages.value;
      setTimeout(() => {
        scrollToBottom();
      }, 0);
    };

    const scrollToBottom = () => {
      window.scrollTo(0, document.body.scrollHeight);
    };

    const applyStyles = (htmlContent: string) => {

      return htmlContent.replace(
        /<img/g,
        '<img style="width: 20%; height: 20%;"'
      );
    };

    return {
      currentPage,
      totalPages,
      slicedData,
      startFloor,
      itemsPerPage: props.itemsPerPage,
      scrollToTop,
      goToLatest,
      scrollToBottom,
      applyStyles,
    };
  },
});
</script>

<style scoped>
.pagination {
  padding: 15px;
  display: flex;
  justify-content: center;
}

.returnbutton {
  text-align: center;
  padding: 15px;
}

.returnbutton .btn {
  font-size: 18px;
  color: rgb(33, 89, 168);
  border-color: rgb(33, 89, 168);
}

.returnbutton .btn:hover {
  background-color: rgba(173,
      216,
      230,
      0.5);
  color: rgb(0, 0, 0);
  border-color: rgb(33, 89, 168);
}

.title {
  color: rgb(94, 94, 94);
  font-size: 3vw;
  font-weight: bold;
  padding: 1%;
}

.title a {
  color: rgb(33, 89, 168);
  text-decoration: none;
}

.title a:hover {
  color: blue;
  text-decoration: underline;
}

.table {
  border: 2px solid rgb(226, 226, 226);
}

.tableleftone {
  background-color: rgb(173, 204, 255);
}

.tablerightone {
  background-color: rgb(252, 252, 252);
}

.tableleft {
  background-color: rgb(239, 243, 190);
}

.tableright {
  background-color: rgb(252, 252, 252);
}

span {
  font-size: 12px;
}

.player {
  text-align: center;
}

.player img {
  width: 100%;
  max-width: 100px;
  height: auto;
}

.nickname a {
  color: rgb(33, 89, 168);
  text-decoration: none;
  font-size: 1.6vw;
}

.nickname a:hover {
  color: blue;
  text-decoration: underline;
}

.nickname,
.level,
.lefticon {
  text-align: center;
  margin-top: 1%;
}

.peoples {
  text-align: center;
  font-weight: bold;
  font-size: 1vw;
}

.peoples span {
  color: rgb(115, 115, 115);
}

.options {
  text-align: right;
  font-size: 1vw;
}

.level {
  font-size: 1.1vw;
  color: rgb(94, 94, 94);
  font-weight: bold;
}

.btn {
  font-size: 1vw;
  background-color: rgba(255, 255, 255, 0.5);
  color: #656565;
  transition: all 0.1s ease;
  border: 0.1px solid #dedede;
}

.btn:hover {
  transform: scale(1.01);
  background-color: #ffffff;
}

.tdcontent {
  word-wrap: break-word;
  font-size: 1.5vw;
}

.tdcontent img {
  width: 20%;
  height: 20%;
}

@media screen and (max-width: 652px) {
  .nickname a {
    font-size: 3vw;
  }

  .level {
    font-size: 2vw;
  }

  .lefticon .btn {
    font-size: 1vw;
  }

  .peoples {
    font-size: 3.5vw;
  }

  .tdcontent {
    font-size: 2.5vw;
  }

  .btn {
    font-size: 1.3vw;
  }
}
</style>