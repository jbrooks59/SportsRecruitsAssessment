<template>
  <div class="container">
    <AcademicFitReport :athlete="athleteInfo" />
    <DataTable :athlete="athleteInfo" />
  </div>
</template>

<script>
import { ref } from "vue";
import AcademicFitReport from "@/components/AcademicFitReport.vue";
import AthleteData from "@/assets/data.json";
import DataTable from "@/components/DataTable.vue";

export default {
  name: "app",
  components: {
    AcademicFitReport,
    DataTable,
  },
  setup() {
    const athleteInfo = ref(AthleteData.data[0]);

    return {
      athleteInfo,
    };
  },
};
</script>
<style>
html {
  font-family: "docs-Roboto", Arial;
}
</style>