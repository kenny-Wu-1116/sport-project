<template>
  <div class="rounded-container">
    <table class="table table-bordered">
      <tbody>
        <tr>
          <th :rowspan="expanded ? tableData.length + 1 : 6" scope="row">
            <img :src="image" style="width: 100%" />
            <div class="1" style="margin-top: 10px">
              <h6 style="text-align: center">{{ name }}</h6>
            </div>

            <div class="2">
              <p style="text-align: center">{{ rate }}</p>
              <h4 style="text-align: center">{{ winRate }}</h4>
            </div>

            <div class="3" style="margin-top: 50px">
              <h5 style="text-align: center">{{ bonus }}{{ dollar }}</h5>
            </div>
          </th>
          <td colspan="4" class="table-title">{{ title }}</td>
        </tr>
        <tr v-for="(row, index) in tableData" :key="index">
          <template v-if="index < 5 || expanded">
            <td v-for="(cell, cellIndex) in row" :key="cellIndex">
              <template v-if="cellIndex === row.length - 1">
                <img :src="cell" alt="比賽圖片" style="width: 25px; height: 25px;" />
              </template>
              <template v-else>
                {{ cell }}
              </template>
            </td>
          </template>
        </tr>
      </tbody>
    </table>
    <div class="text-center">
      <button v-if="!expanded && tableData.length > 5" @click="expandTable">
        <i class="bi bi-caret-down-fill"></i>
      </button>
      <button v-if="expanded" @click="collapseTable">
        <i class="bi bi-caret-up-fill"></i>
      </button>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, type PropType, ref } from "vue";

export default defineComponent({
  name: "Table",
  props: {
    image: {
      type: String,
      required: true,
    },
    name: {
      type: String,
      required: true,
    },
    winRate: {
      type: String,
      required: true,
    },
    rate: {
      type: String,
      default: "評選勝率",
    },
    bonus: {
      type: String,
      required: true,
    },
    dollar: {
      type: String,
      default: "元噱幣",
    },
    title: {
      type: String,
      required: true,
    },
    tableData: {
      type: Array as PropType<any[][]>,
      required: true,
    },
  },
  setup() {
    const expanded = ref(false);

    const expandTable = () => {
      expanded.value = true;
    };

    const collapseTable = () => {
      expanded.value = false;
    };

    return {
      expanded,
      expandTable,
      collapseTable,
    };
  },
});
</script>


<style scoped>
.table-title {
  font-size: 20px;
  color: rgb(187, 154, 37);
  font-weight: bold;
}

.rounded-container {
  border-radius: 10px;
  overflow: hidden;
  border: 1px solid #ced4da;
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.2);
  background-color: white;
}

.table-bordered tbody tr:nth-child(even) td {
  background-color: #fff;
}

.table-bordered tbody tr:nth-child(odd) td {
  background-color: #f6f4f4;
}

.table {
  width: 100%;
  border-collapse: collapse;
  border-radius: 10px;
  border: 1px solid #ced4da;
}

th:hover {
  transform: scale(1.03);
  transition: transform 0.3s ease;
  cursor: pointer;
}

th,
td {
  padding: 16px;
  font-size: 14px;
}

button {
  border: none;
  background-color: transparent;
}

button:hover {
  background-color: initial;
  color: #000;
  transform: scale(1.3);
}

.rounded-container button {
  font-size: 30px;
}

@media screen and (max-width: 900px) {
  .rounded-container {
    font-size: 12px;
  }

  .rounded-container button {
    font-size: 20px;
  }

  th,
  td {
    padding: 10px;
  }
}

@media screen and (max-width: 768px) {
  .rounded-container {
    font-size: 10px;
  }

  .rounded-container button {
    font-size: 16px;
  }

  h4 {
    font-size: 12px;
  }

  h5 {
    font-size: 12px;
  }

  h6 {
    font-size: 12px;
  }

  th,
  td {
    padding: 8px;
    font-size: 12px;
  }

  .table-title {
    font-size: 15px;
  }
}

@media screen and (max-width: 550px) {
  h4 {
    font-size: 10px;
  }

  h5 {
    font-size: 10px;
  }

  h6 {
    font-size: 10px;
  }

  th,
  td {
    padding: 5px;
    font-size: 9px;
  }
}
</style>