<template>
    <div>
        <div class="row">
          <div>{{ athleteGpa.min }}</div>
          <div>{{ athleteGpa["25%"] }}</div>
          <div :style="{ background: gpaColor }">{{ athleteGpa["50%"] }}</div>
          <div>{{ athleteGpa["75%"] }}</div>
          <div>{{ athleteGpa.max }}</div>
        </div>
    </div>
</template>
<script>
import { computed } from "vue";
import { defineComponent } from "vue";

export default defineComponent({
    name: "GPA",
    props: {
        athleteGpa: {
            type: Object,
            required: false,
        },
        athlete: {
            type: Object,
            required: false,
        },
    },
    setup(props) {
      const athleteReport = computed(() => props.athlete.report);
      const gpaColor = computed(() => {
        const difference = props.athleteGpa["50%"] - props.athlete.gpa;
        if (difference > 0.1) {
          return "#d7737d";
        } else if (difference <= 0.1 && difference > 0) {
          return "#c194b5";
        } else if (difference === 0) {
          return "#b4a7d6";
        } else if (difference >= -0.1 && difference < 0) {
          return "#9fa9db"
        } else if (difference < -0.1 && difference >= -0.2) {
          return "#a6a8da";
        } else if (difference < -0.2) {
          return "#75ace5";
        }
      });

      return {
        athleteReport,
        gpaColor,
      };
    },
});
</script>
<style scoped>
.row {
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  width: 100%;
}
</style>