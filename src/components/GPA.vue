<template>
  <div>
    <div style="margin-top: -14px" v-if="index === 0" class="row" :style="{ color: 'white' }">
      <div class="head text">Min</div>
      <div class="head text">25%</div>
      <div class="head text">50%</div>
      <div class="head text">75%</div>
      <div class="head">Max</div>
    </div>
    <div class="row">
      <div class="gpa text">{{ athleteGpa.min }}</div>
      <div class="gpa text">{{ athleteGpa["25%"] }}</div>
      <div style="width: 30px" class="gpa text" :style="{ background: gpaColor }">{{ athleteGpa["50%"] }}</div>
      <div class="gpa text">{{ athleteGpa["75%"] }}</div>
      <div class="gpa">{{ athleteGpa.max }}</div>
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
        index: {
          type: Number,
          required: false,
        }
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
  grid-template-columns: repeat(5, 1fr);
  width: 100%;
}
.text {
  margin-right: 5px;
  justify-self: center;
}
.head {
  justify-self: center;
}
.gpa {
  padding: 10px 0;
  justify-self: center;
}
</style>