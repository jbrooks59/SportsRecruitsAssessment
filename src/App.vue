<template>
  <div class="container">
    <AcademicFitReport :athlete="athleteInfo" />
    <DataTable :athlete="athleteInfo" />
    <div class="belowInfo">
      <div>*Rankings for Division I schools based on NCAA data (www.ncaa.com) and rankings for Division II & III schools are based on data from Hero Sports (www.herosports.com/rankings)</div>
      <div>** GPA is based on SportsRecruits members who have shown interest in (favorited) the school and have provided their GPA on their profile</div>
      <div>***SAT and ACT scores based on national data provided by the National Center of Education Statistics- https://nces.ed.gov/ipeds/</div>
    </div>
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
.container {
  @media (min-width: 1800px) {
    width: 75%;
  }
}
.belowInfo {
  margin-top: 200px;
  font-size: 16px;
}
</style>