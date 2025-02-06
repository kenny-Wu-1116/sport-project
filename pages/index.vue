<template>
  <div v-for="(sportData, sportIndex) in sportsData" :key="'sport_' + sportIndex">
    <div class="container mt-5">
      <div class="sidebar">
        <h2>{{ sportData.title }}</h2>
        <SidebarHome :sidebarItems="sportData.sidebarItems" />
      </div>
      <div class="main-content mt-5">
        <div v-for="(tableData, tableIndex) in sportData.tables" :key="'table_' + tableIndex">
          <TableHome :tableData="tableData.data" :image="tableData.image" :name="tableData.name"
            :winRate="tableData.winRate" :bonus="tableData.bonus" :title="tableData.title" />
          <template v-if="tableIndex !== sportData.tables.length - 1">
            <div class="table-spacing"></div>
          </template>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from "vue";

interface TableData {
  data: string[][];
  image: string;
  name: string;
  winRate: string;
  bonus: string;
  title: string;
}

interface SportData {
  title: string;
  sidebarItems: { name: string; text: string; link: string }[];
  tables: TableData[];
}

export default defineComponent({
  setup() {
    // NBA data
    const nbaData: SportData = {
      title: "NBA",
      sidebarItems: [
        { name: "張志明", text: "熱門討論區", link: "/forumdetail?id=nba1" },
        { name: "王大明", text: "球隊攻防分析", link: "/forumdetail?id=nba2" },
        { name: "陳小龍", text: "近期勝率對比", link: "/forumdetail?id=nba3" },
        { name: "李佳穎", text: "明星球員表現", link: "/forumdetail?id=nba4" },
        { name: "何俊傑", text: "最新比賽資訊", link: "/forumdetail?id=nba5" },
        { name: "周采妮", text: "專家分析推薦", link: "/forumdetail?id=nba6" },
      ],
      tables: [
        {
          data: [
            ["今天", "金州勇士 vs 洛杉磯湖人(主)", "勇士讓 4 分贏 55%", "https://picsum.photos/100/100"],
            ["今天", "芝加哥公牛 vs 邁阿密熱火(主)", "熱火受讓 2 分贏 60%", "https://picsum.photos/100/100"],
            ["今天", "達拉斯獨行俠 vs 波特蘭拓荒者(主)", "獨行俠讓 3 分贏 58%", "https://picsum.photos/100/100"],
            ["昨天", "波士頓塞爾提克 vs 費城 76 人(主)", "塞爾提克讓 5 分贏 52%", "https://picsum.photos/100/100"],
            ["昨天", "丹佛金塊 vs 鳳凰城太陽(主)", "金塊讓 3 分輸 48%", "https://picsum.photos/100/100"],
            ["04/10", "洛杉磯快艇 vs 明尼蘇達灰狼(主)", "快艇讓 1.5 分贏 54%", "https://picsum.photos/100/100"],
            ["04/09", "紐約尼克 vs 布魯克林籃網(主)", "尼克受讓 2 分贏 57%", "https://picsum.photos/100/100"],
            ["04/08", "聖安東尼奧馬刺 vs 夏洛特黃蜂(主)", "黃蜂受讓 4 分輸 45%", "https://picsum.photos/100/100"],
            ["04/07", "奧蘭多魔術 vs 休士頓火箭(主)", "火箭讓 3 分贏 50%", "https://picsum.photos/100/100"],
          ],
          image: "https://picsum.photos/50/50",
          name: "劉建國",
          winRate: "63%",
          bonus: "85",
          title: "NBA 近 30 日 勝率 75%",
        },
        {
          data: [
            ["今天", "洛杉磯湖人 vs 丹佛金塊(主)", "湖人讓 3 分贏 56%", "https://picsum.photos/100/100"],
            ["今天", "布魯克林籃網 vs 多倫多暴龍(主)", "暴龍受讓 1.5 分贏 59%", "https://picsum.photos/100/100"],
            ["今天", "鳳凰城太陽 vs 曼菲斯灰熊(主)", "太陽讓 2 分輸 47%", "https://picsum.photos/100/100"],
            ["昨天", "芝加哥公牛 vs 印第安那溜馬(主)", "公牛讓 5 分贏 53%", "https://picsum.photos/100/100"],
            ["昨天", "達拉斯獨行俠 vs 休士頓火箭(主)", "獨行俠讓 4 分輸 49%", "https://picsum.photos/100/100"],
            ["04/10", "波士頓塞爾提克 vs 邁阿密熱火(主)", "熱火受讓 2.5 分贏 55%", "https://picsum.photos/100/100"],
            ["04/09", "金州勇士 vs 洛杉磯快艇(主)", "勇士讓 3 分贏 58%", "https://picsum.photos/100/100"],
            ["04/08", "奧蘭多魔術 vs 紐約尼克(主)", "尼克受讓 1.5 分輸 44%", "https://picsum.photos/100/100"],
            ["04/07", "聖安東尼奧馬刺 vs 夏洛特黃蜂(主)", "黃蜂讓 3 分贏 51%", "https://picsum.photos/100/100"],
          ],
          image: "https://picsum.photos/50/50",
          name: "陳柏安",
          winRate: "64%",
          bonus: "88",
          title: "NBA 近 30 日 勝率 77%",
        }

      ],
    };

    const mlbData: SportData = {
      title: "MLB",
      sidebarItems: [
        { name: "鄭文豪", text: "球隊近況解析", link: "/forumdetail?id=mlb1" },
        { name: "許佩珊", text: "投手與打者數據", link: "/forumdetail?id=mlb2" },
        { name: "楊宗翰", text: "近期排名與戰績", link: "/forumdetail?id=mlb3" },
        { name: "林美玲", text: "大數據勝率分析", link: "/forumdetail?id=mlb4" },
        { name: "陳志明", text: "球員表現分析", link: "/forumdetail?id=mlb5" } // Changed new item
      ],

      tables: [
        {
          data: [
            ["今天", "紐約洋基 vs 波士頓紅襪(主)", "洋基讓 1.5 分贏 58%", "https://picsum.photos/100/100"],
            ["今天", "洛杉磯道奇 vs 休士頓太空人(主)", "道奇讓 2 分贏 60%", "https://picsum.photos/100/100"],
            ["今天", "聖地牙哥教士 vs 舊金山巨人(主)", "教士受讓 1.5 分贏 55%", "https://picsum.photos/100/100"],
            ["昨天", "亞特蘭大勇士 vs 費城費城人(主)", "費城人受讓 1 分贏 55%", "https://picsum.photos/100/100"],
            ["昨天", "芝加哥小熊 vs 聖路易紅雀(主)", "小熊讓 1.5 分輸 50%", "https://picsum.photos/100/100"],
            ["04/10", "西雅圖水手 vs 德州遊騎兵(主)", "水手讓 1 分贏 53%", "https://picsum.photos/100/100"],
            ["04/09", "巴爾的摩金鶯 vs 坦帕灣光芒(主)", "光芒受讓 2 分輸 47%", "https://picsum.photos/100/100"],
            ["04/08", "科羅拉多落磯山 vs 洛杉磯天使(主)", "天使讓 2 分贏 56%", "https://picsum.photos/100/100"],
            ["04/07", "辛辛那提紅人 vs 匹茲堡海盜(主)", "海盜受讓 1 分輸 48%", "https://picsum.photos/100/100"],
          ],
          image: "https://picsum.photos/50/50",
          name: "高志偉",
          winRate: "66%",
          bonus: "90",
          title: "MLB 近 30 日 勝率 78%",
        },
      ],
    };

    const sportsData = ref<SportData[]>([nbaData, mlbData]);
    return {
      sportsData,
    };
  },
});
</script>

<style scoped>
.container {
  display: flex;
  max-width: 1000px;
}

.sidebar {
  flex: 1;
  margin-right: 15px;
}

.main-content {
  flex: 3;
  margin-left: 15px;
}

.table-spacing {
  padding: 20px;

}

@media screen and (max-width: 768px) {
  .sidebar {
    margin-right: 2px;
  }

  .main-content {
    margin-left: 2px;
  }
}
</style>