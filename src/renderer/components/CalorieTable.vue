<template>
  <div class="table" v-if="store.hasLoaded">
    <table>
      <tr>
        <th>Monday</th>
        <th>Tuesday</th>
        <th>Wednesday</th>
        <th>Thursday</th>
        <th>Friday</th>
        <th>Saturday</th>
        <th>Sunday</th>
      </tr>
      <tr>
        <td v-for="data in summaryData">
          {{ data.totalCalories }}kcal ({{
            (
              ((data.totalCalories - config.calories) * 100) /
              config.calories
            ).toFixed(0)
          }}%)
        </td>
      </tr>
      <tr>
        <td v-for="data in summaryData">
          {{ data.totalCarbs }}g ({{
            (((data.totalCarbs - config.carbs) * 100) / config.carbs).toFixed(
              0
            )
          }}%)
        </td>
      </tr>
      <tr>
        <td v-for="data in summaryData">
          {{ data.totalFats }}g ({{
            (((data.totalFats - config.fats) * 100) / config.fats).toFixed(0)
          }}%)
        </td>
      </tr>
      <tr>
        <td v-for="data in summaryData">
          {{ data.totalProtein }}g ({{
            (
              ((data.totalProtein - config.protein) * 100) /
              config.protein
            ).toFixed(0)
          }}%)
        </td>
      </tr>
    </table>
  </div>
</template>

<script lang="ts">
import { computed, defineComponent } from "vue";
import getDaysSummary from "../helpers/GetDaysData";
import { useStore } from "../store";

export default defineComponent({
  setup() {
    const store = useStore();
    const summaryData = computed(() => {
      return getDaysSummary(store.data);
    });
    const config = computed(() => {
      return store.config!;
    });
    return { store, summaryData, config };
  },
  // computed: {
  //   summaryData: function () {
  //     return getDaysSummary(this.store.data);
  //   },
  //   config() {
  //     return this.store.config!;
  //   },
  // },
});
</script>

<style lang="scss" scoped>
@import "../styles/table-style.scss";
</style>
