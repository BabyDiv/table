<template>
  <div class="table">
    <div class="table__tabs">
      <button
        class="table__tab-button"
        :class="{ 'table__tab-button--active': activeTab === 'recent' }"
        @click="activeTab = 'recent'"
      >
        Последние игры
      </button>
      <button
        class="table__tab-button"
        :class="{ 'table__tab-button--active': activeTab === 'season' }"
        @click="activeTab = 'season'"
      >
        Статистика сезона
      </button>
    </div>

    <div v-if="activeTab === 'recent'" class="table__content">
      <table class="table__element">
        <thead class="table__head">
          <tr class="table__row">
            <th class="table__cell table__cell--head">Матч</th>
            <th class="table__cell table__cell--head">G</th>
            <th class="table__cell table__cell--head">P</th>
            <th class="table__cell table__cell--head">PM</th>
            <th class="table__cell table__cell--head">PIM</th>
            <th class="table__cell table__cell--head">PP</th>
            <th class="table__cell table__cell--head">FO</th>
            <th class="table__cell table__cell--head">Время</th>
            <th class="table__cell table__cell--head">SOG</th>
          </tr>
        </thead>
        <tbody class="table__body">
          <tr class="table__row" v-for="(game, index) in recent_games" :key="index">
            <td class="table__cell">{{ game.match }}</td>
            <td class="table__cell">{{ game.G }}</td>
            <td class="table__cell">{{ game.P }}</td>
            <td class="table__cell">{{ game.PM }}</td>
            <td class="table__cell">{{ game.PIM }}</td>
            <td class="table__cell">{{ game.PP }}</td>
            <td class="table__cell">{{ game.FO }}</td>
            <td class="table__cell">{{ game.ice_time }}</td>
            <td class="table__cell">{{ game.SOG }}</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div v-if="activeTab === 'season'" class="table__content">
      <table class="table__element">
        <thead class="table__head">
          <tr class="table__row">
            <th class="table__cell table__cell--head">Сезон</th>
            <th class="table__cell table__cell--head">Команда</th>
            <th class="table__cell table__cell--head">GP</th>
            <th class="table__cell table__cell--head">G</th>
            <th class="table__cell table__cell--head">A</th>
            <th class="table__cell table__cell--head">P</th>
            <th class="table__cell table__cell--head">PM</th>
            <th class="table__cell table__cell--head">PIM</th>
            <th class="table__cell table__cell--head">Время</th>
          </tr>
        </thead>
        <tbody class="table__body">
          <tr class="table__row" v-for="(season, index) in seasonStats" :key="'season-' + index">
            <td class="table__cell">{{ season.season }}</td>
            <td class="table__cell">{{ season.team }}</td>
            <td class="table__cell">{{ season.GP }}</td>
            <td class="table__cell">{{ season.G }}</td>
            <td class="table__cell">{{ season.A }}</td>
            <td class="table__cell">{{ season.P }}</td>
            <td class="table__cell">{{ season.PM }}</td>
            <td class="table__cell">{{ season.PIM }}</td>
            <td class="table__cell">{{ season.ice_time }}</td>
          </tr>
        </tbody>
      </table>

      
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        activeTab: 'recent',
        recent_games: [
          {
            match: "Трактор 3:2 АК Барс",
            G: 23,
            P: 67,
            PM: 17,
            PIM: 17,
            PP: "1/3",
            FO: "2/5",
            ice_time: "18:47",
            SOG: "5/7"
          },
          {
            match: "Трактор 3:2 АК Барс",
            G: 23,
            P: 67,
            PM: 17,
            PIM: 17,
            PP: "1/3",
            FO: "2/5",
            ice_time: "18:47",
            SOG: "5/7"
          },
          {
            match: "Трактор 3:2 АК Барс",
            G: 23,
            P: 67,
            PM: 17,
            PIM: 17,
            PP: "1/3",
            FO: "2/5",
            ice_time: "18:47",
            SOG: "5/7"
          },
          {
            match: "Трактор 3:2 АК Барс",
            G: 23,
            P: 67,
            PM: 17,
            PIM: 17,
            PP: "1/3",
            FO: "2/5",
            ice_time: "18:47",
            SOG: "5/7"
          }
        ],
        seasonStats: [
          {
            season: 1,
            team: "Трактор",
            GP: 67,
            G: 23,
            A: 17,
            P: 67,
            PM: 17,
            PIM: 17,
            ice_time: "18:47"
          },
          {
            season: 6,
            team: "Трактор",
            GP: 67,
            G: 23,
            A: 17,
            P: 67,
            PM: 17,
            PIM: 17,
            ice_time: "18:47"
          },
          {
            season: 1,
            team: "Трактор",
            GP: 67,
            G: 23,
            A: 17,
            P: 67,
            PM: 17,
            PIM: 17,
            ice_time: "18:47"
          },
          {
            season: 6,
            team: "Трактор",
            GP: 67,
            G: 23,
            A: 17,
            P: 67,
            PM: 17,
            PIM: 17,
            ice_time: "18:47"
          }
        ]
      };
    }
  };
</script>

