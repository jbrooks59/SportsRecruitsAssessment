<template>
    <div>
      <div class="data-table">
        <div class="row header-row">
          <div class="cell">School</div>
          <div class="cell">Division</div>
          <div class="cell">Conference</div>
          <div class="cell">Ranking</div>
          <div class="cell">GPA</div>
          <div class="cell">SAT Reading</div>
          <div class="cell">SAT Math</div>
          <div class="cell">ACT</div>
        </div>
        <div class="row" v-for="(athlete, index) in athleteReport" :key="index" :class="{ 'even-row': index % 2 === 1 }">
          <div class="cell">{{ athlete.school }}</div>
          <div class="cell">{{ athlete.division }}</div>
          <div class="cell">{{ athlete.conference }}</div>
          <div class="cell">{{ athlete.ranking }}</div>
          <div class="cell">
            <GPA :athlete="athleteInfo" :athleteGpa="athlete.gpa" />
          </div>
          <div class="cell">{{ athlete.sat.reading.min === "N/A" ? "Not Reported" : `${athlete.sat.reading.min}-${athlete.sat.reading.max}` }}</div>
          <div class="cell">{{ athlete.sat.math.min === "N/A" ? "Not Reported" : `${athlete.sat.math.min}-${athlete.sat.math.max}` }}</div>
          <div class="cell">{{ athlete.act.min === "N/A" ? "Not Reported" : `${athlete.act.min}-${athlete.act.max}` }}</div>
        </div>
      </div>
    </div>
</template>

<script>
import { computed, ref } from "vue";
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
        const testingScores = computed(() => {

        })

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
  grid-template-columns: 253px 75px 253px 75px repeat(4, 1fr);
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
.even-row > .cell {
  background-color: #d5e7ff;
}
@media (max-width: 1024px) {
  .data-table {
    overflow-x: scroll;
  }
  .row {
    width: 150%;
  }
}
</style>
