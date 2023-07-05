<template>
  <div>
    <div class="data-table">
      <div class="row header-row">
        <div class="cell">School</div>
        <div class="cell">Division</div>
        <div class="cell">Conference</div>
        <div class="cell">Ranking<br>(DI NCAA)<br>(DII & DIII Hero Sports)</div>
        <div style="justify-self: center" class="cell">GPA**</div>
        <div class="cell">SAT Reading***<br>25%-75%</div>
        <div class="cell">SAT Math***<br>25%-75%</div>
        <div class="cell">ACT Composite***<br>25%-75%</div>
      </div>
      <div class="row" v-for="(athlete, index) in athleteReport" :key="index" :class="{ 'even-row': index % 2 === 1 }">
        <div class="cell">{{ athlete.school }}</div>
        <div class="cell">{{ athlete.division }}</div>
        <div class="cell">{{ athlete.conference }}</div>
        <div class="cell">{{ athlete.ranking }}</div>
        <div class="gpa cell" :class="{'first-row': index === 0 }">
          <GPA :index="index" :athlete="athleteInfo" :athleteGpa="athlete.gpa" />
        </div>
        <div class="cell">{{ athlete.sat.reading.min === "N/A" ? "Not Reported" : `${athlete.sat.reading.min}-${athlete.sat.reading.max}` }}</div>
        <div class="cell">{{ athlete.sat.math.min === "N/A" ? "Not Reported" : `${athlete.sat.math.min}-${athlete.sat.math.max}` }}</div>
        <div class="cell">{{ athlete.act.min === "N/A" ? "Not Reported" : `${athlete.act.min}-${athlete.act.max}` }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { computed } from "vue";
import { defineComponent } from "vue";
import GPA from "@/components/GPA.vue";

export default defineComponent({
  name: "DataTable",
  components: {
    GPA,
  },
  props: {
    athlete: {
      type: Object,
      required: false,
    },
  },
  setup(props) {
    const athleteInfo = computed(() => props.athlete);
    const athleteReport = computed(() => props.athlete.report);

    return {
      athleteInfo,
      athleteReport,
    };
  },
});
</script>
<style scoped>
.data-table {
  display: grid;
  grid-gap: 0;
  width: 100%;
  overflow-x: auto;
}
.row {
  display: grid;
  grid-template-columns: 253px 75px 280px 150px repeat(4, 1fr);
  width: 100%;
}
.header-row {
  background-color: black;
  color: white;
  font-weight: bold;
}
.row > .cell {
  padding: 10px;
  font-size: 9pt;
}
.gpa.cell {
  padding: 0;
}
.even-row > .cell {
  background-color: #d5e7ff;
}
.first-row {
  padding: 0 !important;
}
@media (max-width: 1080px) {
  .data-table {
    overflow-x: scroll;
  }
  .row {
    width: 150%;
  }
}
</style>