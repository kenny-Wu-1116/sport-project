<template>
  <div class="menubox">
    <div class="menubox-con">
      <div class="tagbox-container">
        <div class="tagbox-left">
          <div class="tagbox-horizontal" v-for="(category, index) in sportCategories" :key="index">
            <div class="tagbox-first">
              <ol class="tag-league">
                <li>
                  <span class="badge rounded-pill bg-secondary" :class="{ 'active': selectedSport === category.name }"
                    @click="handleSportClick(category.name)">{{ category.name }}</span>
                </li>
              </ol>
            </div>
            <div class="tagbox-last">
              <ol class="tag-con">
                <li v-for="(sport, sportIndex) in category.sports" :key="sportIndex">
                  <button type="button" class="btn btn-light tag-btn"
                    :class="{ 'active': selectedSport === sport.name }" @click="handleSportClick(sport.name)">
                    {{ sport.name }}
                  </button>
                </li>
              </ol>
            </div>
          </div>
        </div>
        <div class="tagbox-right">
          <div class="datebox-first">
            <ol class="tag-date">
              <li><span class="badge bg-secondary badge-date">{{ dateLabel }}</span></li>
            </ol>
          </div>
          <div class="datebox-last">
            <ol class="date-con">
              <li v-for="(date, dateIndex) in dates" :key="dateIndex" @click="handleDateClick(date)">
                <div :class="{ 'date-item': true, 'active': selectedDate === date }">
                  <p>{{ date }}</p>
                  <strong>{{ dayOfWeek[dateIndex] }}</strong>
                </div>
              </li>
            </ol>
          </div>
        </div>
      </div>
    </div>
  </div>
  <table border="1" cellspacing="0" cellpadding="0" class="predictgame-table">
    <tbody>
      <tr>
        <th rowspan="2" scope="col" class="th-gameinfo">{{ matchInfoLabel }}</th>
        <th rowspan="2" scope="col" class="th-teaminfo">{{ teamInfoLabel }}</th>
        <th colspan="2" scope="col" class="th-universal">{{ universalLabel }}</th>
        <th colspan="3" scope="col" class="th-bank">{{ bankLabel }}</th>
      </tr>
      <tr>
        <th class="th-universal-bet01">{{ handicapLabel }}</th>
        <th class="th-universal-bet02">{{ sizeLabel }}</th>
        <th class="th-bank-bet01">{{ bankHandicapLabel }}</th>
        <th class="th-bank-bet03">{{ bankNonHandicapLabel }}</th>
        <th class="th-bank-bet02">{{ bankSizeLabel }}</th>
      </tr>
      <template v-if="filteredGames.length === 0">
        <tr>
          <td colspan="7" class="no-data" scope="row">{{ noDataLabel }}</td>
        </tr>
      </template>
      <template v-for="(game, index) in filteredGames" :key="index">
        <tr>
          <td rowspan="2" class="td-gameinfo">
            <div>
              <h5>{{ game.matchNumber }}</h5>
              <h6>{{ game.time }}</h6>
              <h6><a :href="game.matchInfoLink" class="game-info-link">{{ gameInfoLinkLabel }}</a></h6>
            </div>
          </td>
          <td>
            <div>
              <h6><a :href="game.team1.link">{{ game.team1.name }}</a></h6>
              <p>{{ game.team1.player }}</p>
            </div>
          </td>
          <template v-for="(bet, betIndex) in game.universalBets" :key="betIndex">
            <td>
              <div class="form-check">
                <input class="form-check-input" :type="bet.type" :name="bet.name" :id="bet.id">
                <label class="form-check-label" :for="bet.id">{{ bet.label }}</label>
              </div>
            </td>
          </template>
        </tr>
        <tr>
          <td>
            <div>
              <h6><a :href="game.team2.link">{{ game.team2.name }}</a></h6>
              <p>{{ game.team2.player }}</p>
            </div>
          </td>
          <template v-for="(bet, betIndex) in game.bankBets" :key="betIndex">
            <td>
              <div class="form-check">
                <input class="form-check-input" :type="bet.type" :name="bet.name" :id="bet.id">
                <label class="form-check-label" :for="bet.id">{{ bet.label }}</label>
              </div>
            </td>
          </template>
        </tr>
        <template v-if="index !== filteredGames.length - 1">
          <tr class="gaprow">
            <td colspan="7" scope="row"></td>
          </tr>
        </template>
      </template>
    </tbody>
  </table>
</template>

<script lang="ts">
import { defineComponent, ref, computed, type PropType } from 'vue';

interface Team {
  name: string;
  player: string;
  link: string;
}

interface Bet {
  type: string;
  name: string;
  id: string;
  label: string;
}

interface Game {
  matchNumber: string;
  date: string;
  time: string;
  matchInfoLink: string;
  team1: Team;
  team2: Team;
  universalBets: Bet[];
  bankBets: Bet[];
  sport: string;
}

interface Sport {
  name: string;
}

interface SportCategory {
  name: string;
  sports: Sport[];
}

export default defineComponent({
  props: {
    sportCategories: {
      type: Array as PropType<SportCategory[]>,
      required: true
    },
    dates: {
      type: Array as PropType<string[]>,
      required: true
    },
    dayOfWeek: {
      type: Array as PropType<string[]>,
      required: true
    },
    gamesData: {
      type: Array as PropType<Game[]>,
      required: true
    },

    matchInfoLabel: {
      type: String,
      default: '賽事資訊'
    },
    teamInfoLabel: {
      type: String,
      default: '球隊資訊'
    },
    universalLabel: {
      type: String,
      default: '國際盤'
    },
    bankLabel: {
      type: String,
      default: '運彩盤'
    },
    handicapLabel: {
      type: String,
      default: '讓分'
    },
    sizeLabel: {
      type: String,
      default: '大小'
    },
    bankHandicapLabel: {
      type: String,
      default: '讓分'
    },
    bankNonHandicapLabel: {
      type: String,
      default: '不讓分'
    },
    bankSizeLabel: {
      type: String,
      default: '大小'
    },
    noDataLabel: {
      type: String,
      default: '暂無數據'
    },
    gameInfoLinkLabel: {
      type: String,
      default: '對戰資訊'
    },
    dateLabel: {
      type: String,
      default: '日期'
    }
  },
  setup(props) {
    const selectedSport = ref<string>('MLB');
    const selectedDate = ref<string>('04/19');

    const filteredGames = computed(() => {
      return props.gamesData.filter((game: Game) => {
        return game.sport === selectedSport.value && game.date === selectedDate.value;
      });
    });

    const handleSportClick = (sport: string) => {
      selectedSport.value = sport;
    };

    const handleDateClick = (date: string) => {
      selectedDate.value = date;
    };

    return { selectedSport, selectedDate, filteredGames, handleSportClick, handleDateClick };
  }
});
</script>

<style scoped>
.date-item.active {
  background-color: #ffed4a;
  cursor: pointer;
}

.game-info-link {
  text-decoration: underline;
  color: blue;
  font-size: 12px;
}

a {
  text-decoration: none;
  color: black;
  font-weight: bold;
}

.tag-btn.active {
  background-color: #f5df1f;
  font-weight: bold;
}

.menubox-con {
  background: linear-gradient(to bottom,
      rgb(233, 233, 233),
      rgb(248, 248, 248));
}

.tagbox-container {
  display: flex;
  flex-wrap: wrap;
}

.tagbox-left {
  margin-top: 15px;
  flex: 12;
}

.tagbox-right {
  margin-top: 15px;
  flex: 5;
}

.tagbox-horizontal {
  display: flex;
}

.tag-league {
  font-size: 20px;
}

.tag-con {
  display: flex;
}

.tag-con li {
  margin-right: 5px;
}

.tag-league,
.tag-con {
  list-style: none;
}

.date-con {
  display: flex;
  text-align: center;
}

.date-con li {
  margin-right: 20px;
}

.tag-date,
.date-con {
  list-style-type: none;
}


.badge-date {
  font-size: 16px;
  width: 95%;
}

.tag-btn {
  background-color: #d8d8d8;
  font-size: 14px;
}

.tag-btn:hover {
  background-color: #f5df1f;
}

.date-con {
  display: flex;
  justify-content: space-around;
}

.date-item {
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 8px;
  padding: 8px;
}

.date-item:hover {
  background-color: #ffed4a;
  cursor: pointer;
}

.predictgame-table {
  width: 100%;
  border-collapse: collapse;
}

.predictgame-table th,
.predictgame-table td {
  border: 1px solid #cbcbcb;
  padding: 5px;
}

.gaprow {
  border-top: 1px solid #000;
}

.th-gameinfo,
.th-teaminfo {
  background-color: rgb(61, 186, 224);
  color: white;
  text-align: center;
}

.th-universal,
.th-universal-bet01,
.th-universal-bet02 {
  background-color: rgb(47, 192, 47);
  color: white;
  text-align: center;
}

.th-bank,
.th-bank-bet01,
.th-bank-bet02,
.th-bank-bet03 {
  background-color: rgb(73, 145, 207);
  color: white;
  text-align: center;
}

.predictgame-table th,
.predictgame-table td {
  font-size: 12px;
  padding: 3px;
}

.date-con li {
  margin-right: 10px;
}

.tag-btn {
  font-size: 12px;
}

.gaprow {
  background-color: #e9e9e9;
}

.no-data {
  text-align: center;
  font-size: 50px;
  padding: 5px;
}

.predictgame-table {
  width: 100%;
  table-layout: fixed;
}

@media screen and (max-width: 1200px) {

  .tagbox-left,
  .tagbox-right {
    flex: 100%;
    margin-top: 10px;
  }
}

@media screen and (max-width: 992px) {

  .tagbox-left,
  .tagbox-right {
    flex: 100%;
    margin-top: 10px;
  }
}

@media screen and (max-width: 768px) {
  .tagbox-horizontal {
    flex-direction: column;
  }

  .tag-btn {
    font-size: 10px;
  }

  .date-item {
    font-size: 12px;
  }

  h6 {
    font-size: 9.5px;
  }

  .predictgame-table th,
  .predictgame-table td {
    font-size: 10px;
    padding: 5px;
  }
}

@media screen and (max-width: 552px) {
  .tag-btn {
    font-size: 9px;
  }

  a {
    font-size: 12px;
  }

  .predictgame-table th,
  .predictgame-table td {
    font-size: 8px;
    padding: 3px;
  }

  .game-info-link {

    font-size: 10px;
  }
}

.date-item {
  padding: 6px;
}

.td-gameinfo div,
.td-teaminfo div {
  padding: 8px;
}

.td-gameinfo h5 {
  font-size: 14px;
}

.td-teaminfo p {
  font-size: 12px;
}
</style>