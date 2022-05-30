<template>
  <DxChart
    id="chart"
    :data-source="grossProductData"
    :sticky-hovering="false"
    title="Great Lakes Gross State Product"
  >
    <DxCommonSeriesSettings
      type="spline"
      argument-field="state"
      hover-mode="includePoints"
    >
      <DxPoint hover-mode="allArgumentPoints" />
    </DxCommonSeriesSettings>
    <DxSeries
      v-for="year in yearSources"
      :key="year.value"
      :value-field="year.value"
      :color="computeSeriesColor(year.proj)"
    />
    <!-- :name="year.proj" -->

    <!-- <DxLegend
      vertical-alignment="bottom"
      horizontal-alignment="center"
      hover-mode="excludePoints"
    /> -->
    <DxLegend :visible="false" />
    <!-- <DxExport :enabled="true" /> -->
  </DxChart>
</template>
<script>
import {
  DxChart,
  DxCommonSeriesSettings,
  DxSeries,
  // DxExport,
  DxLegend,
  DxPoint,
} from "devextreme-vue/chart";

import { yearSources, grossProductData } from "./data.js";

export default {
  components: {
    DxChart,
    DxCommonSeriesSettings,
    DxSeries,
    // DxExport,
    DxLegend,
    DxPoint,
  },

  data() {
    return {
      yearSources,
      grossProductData,
    };
  },
  methods: {
    computeSeriesColor(proj) {
      // https://js.devexpress.com/Documentation/ApiReference/Common/Utils/viz/#generateColorspalette_count_options
      let _res = "";
      switch (proj) {
        case "2":
          _res = "#00ff00";
          break;

        default:
          _res = null;
          break;
      }
      return _res;
    },
  },
};
</script>
<style>
#chart {
  height: 440px;
}
</style>
