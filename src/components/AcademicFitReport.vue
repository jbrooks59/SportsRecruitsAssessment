<template>
  <div>
    <div class="info">
      <div class="profile-image" :class="{ 'no-image': !athleteProfileImage }">
        <img v-if="athleteProfileImage" :src="athleteProfileImage" alt="Profile Image" />
        <div v-else class="initials">{{ athleteInitials }}</div>
      </div>
      <div class="info-column-one">
        <ul>
          <li class="athlete-name" contenteditable="true" v-on:input="updateAthleteName">{{ athleteName }}</li>
          <li>
            <label>Sport:</label>
            {{ athleteSport }}
          </li>
          <li>
            <label>Class:</label>
            {{ athleteGradYear }}
          </li>
          <li>
            <label>Club:</label>
            {{ athleteClubName }}
          </li>
        </ul>
      </div>
      <div class="info-column-two">
        <ul>
          <li>
            <label>High School:</label>
            {{ athleteHighSchoolName }}
          </li>
          <li>
            <label>GPA:</label>
            {{ athleteGpa }}
          </li>
          <li>
            <label>Desired Major:</label>
            {{ athleteMajor }}
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { computed, ref } from "vue";

export default {
  name: "AcademicFitReport",
  props: {
    athlete: {
      type: Object,
      required: false,
    },
  },
  setup(props) {
    const athleteProfileImage = computed(() => props.athlete.profile_image);
    const athleteName = ref(props.athlete.name);
    const athleteSport = computed(() => props.athlete.sport);
    const athleteGradYear = computed(() => props.athlete.grad_year);
    const athleteClubName = computed(() => props.athlete.club.name);
    const athleteHighSchoolName = computed(
        () => props.athlete.high_school.name
    );
    const athleteGpa = computed(() => props.athlete.gpa);
    const athleteMajor = computed(() => props.athlete.major);
    const athleteInitials = computed(() => {
      const space = athleteName.value.indexOf(" ");
      const firstName = athleteName.value.substring(0, space);
      const lastName = athleteName.value.substring(space + 1);
      return `${firstName.charAt(0)}${lastName.charAt(0)}`;
    });
    const initialsBackgroundColor = computed(() => {
      const space = athleteName.value.indexOf(" ");
      const lastNameInitial = athleteName.value.substring(space + 1).charAt(0).toLowerCase();
      switch (lastNameInitial) {
        case "a":
        case "b":
        case "c":
        case "d":
        case "e":
          return "#f1603c";
        case "f":
        case "g":
        case "h":
        case "i":
        case "j":
          return "#6082fa";
        case "k":
        case "l":
        case "m":
        case "n":
        case "o":
          return "#827cb8";
        case "p":
        case "q":
        case "r":
        case "s":
          return "#0097a4";
        case "t":
        case "u":
        case "v":
        case "w":
          return "#ffe066";
        case "x":
        case "y":
        case "z":
          return "#ffa94d";
        default:
          return "#ccc"
      }
    })

    const updateAthleteName = (event) => {
      const text = event.target.innerText;
      athleteName.value = text.replace(/[\n\r]/g, "").trim();
      setCursorToEnd(event.target);
    };

    const setCursorToEnd = (element) => {
      const range = document.createRange();
      const selection = window.getSelection();
      range.selectNodeContents(element);
      range.collapse(false);
      selection.removeAllRanges();
      selection.addRange(range);
    };

    return {
      athleteProfileImage,
      athleteName,
      athleteSport,
      athleteGradYear,
      athleteClubName,
      athleteHighSchoolName,
      athleteGpa,
      athleteMajor,
      athleteInitials,
      updateAthleteName,
      initialsBackgroundColor
    };
  },
};
</script>
<style scoped>
.info {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-left: 10px;
}

.info img {
  height: 99px;
  width: 98px;
  border-radius: 50%;
  align-self: center;
  margin-bottom: 10px;
}

.profile-image {
  position: relative;
}

.profile-image.no-image {
  width: 98px;
  height: 98px;
  border-radius: 50%;
  background-color: v-bind(initialsBackgroundColor);
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 10px;
}

.profile-image.no-image .initials {
  font-size: 24px;
  font-weight: bold;
  color: #fff;
  text-transform: uppercase;
}

.info-column-one,
.info-column-two {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

.info ul {
  list-style: none;
  padding-left: 10px;
  margin: 0;
}

.info ul li {
  margin-bottom: 10px;
}

.info ul li label {
  font-weight: bold;
}

.info ul li.athlete-name {
  font-size: 16pt;
  font-weight: bold;
  color: #00b4ff;
  margin-bottom: 5px;
}

@media (min-width: 651px) {
  .info {
    flex-direction: row;
    align-items: flex-end;
  }

  .info-column-one,
  .info-column-two {
    flex-direction: column;
    align-items: flex-start;
    margin-bottom: 0;
  }
}
</style>

