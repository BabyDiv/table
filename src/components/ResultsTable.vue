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
        История
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

            <td class="table__cell">
              <span v-if="!editingCell(index, 'G')" @click="startEdit(index, 'G')">{{ game.G }}</span>
              <input
                v-else
                v-model="recent_games[index].G"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'P')" @click="startEdit(index, 'P')">{{ game.P }}</span>
              <input
                v-else
                v-model="recent_games[index].P"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'PM')" @click="startEdit(index, 'PM')">{{ game.PM }}</span>
              <input
                v-else
                v-model="recent_games[index].PM"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'PIM')" @click="startEdit(index, 'PIM')">{{ game.PIM }}</span>
              <input
                v-else
                v-model="recent_games[index].PIM"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'PP')" @click="startEdit(index, 'PP')">{{ game.PP }}</span>
              <input
                v-else
                v-model="recent_games[index].PP"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'FO')" @click="startEdit(index, 'FO')">{{ game.FO }}</span>
              <input
                v-else
                v-model="recent_games[index].FO"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'ice_time')" @click="startEdit(index, 'ice_time')">{{ game.ice_time }}</span>
              <input
                v-else
                v-model="recent_games[index].ice_time"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'SOG')" @click="startEdit(index, 'SOG')">{{ game.SOG }}</span>
              <input
                v-else
                v-model="recent_games[index].SOG"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>
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
            <td class="table__cell">
              <span v-if="!editingCell(index, 'season', 'season')" @click="startEdit(index, 'season', 'season')">
                {{ season.season }}
              </span>
              <input
                v-else
                v-model="seasonStats[index].season"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'team', 'season')" @click="startEdit(index, 'team', 'season')">
                {{ season.team }}
              </span>
              <input
                v-else
                v-model="seasonStats[index].team"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'GP', 'season')" @click="startEdit(index, 'GP', 'season')">
                {{ season.GP }}
              </span>
              <input
                v-else
                v-model="seasonStats[index].GP"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'G', 'season')" @click="startEdit(index, 'G', 'season')">
                {{ season.G }}
              </span>
              <input
                v-else
                v-model="seasonStats[index].G"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'A', 'season')" @click="startEdit(index, 'A', 'season')">
                {{ season.A }}
              </span>
              <input
                v-else
                v-model="seasonStats[index].A"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'P', 'season')" @click="startEdit(index, 'P', 'season')">
                {{ season.P }}
              </span>
              <input
                v-else
                v-model="seasonStats[index].P"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'PM', 'season')" @click="startEdit(index, 'PM', 'season')">
                {{ season.PM }}
              </span>
              <input
                v-else
                v-model="seasonStats[index].PM"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'PIM', 'season')" @click="startEdit(index, 'PIM', 'season')">
                {{ season.PIM }}
              </span>
              <input
                v-else
                v-model="seasonStats[index].PIM"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>

            <td class="table__cell">
              <span v-if="!editingCell(index, 'ice_time', 'season')" @click="startEdit(index, 'ice_time', 'season')">
                {{ season.ice_time }}
              </span>
              <input
                v-else
                v-model="seasonStats[index].ice_time"
                @blur="stopEdit"
                @keyup.enter="stopEdit"
                type="text"
              />
            </td>
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
        editing: { row: null, column: null },
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
    },
    methods: {
      startEdit(row, column) {
        this.editing = { row, column };
      },
      stopEdit() {
        this.editing = { row: null, column: null };
      },
      editingCell(row, column) {
        return this.editing.row === row && this.editing.column === column;
      }
    }
  };
</script>


