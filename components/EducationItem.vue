<template>
  <div class="education-item">
    <div class="education-item__info">
      <h1>{{education.schoolName}}</h1>
      <IconLabel v-if="education.degreeName" icon="bxs-graduation">
        {{education.degreeName}}
      </IconLabel>
      <IconLabel v-if="education.fieldOfStudy" icon="bx-atom">
        {{education.fieldOfStudy}}
      </IconLabel>
      <IconLabel
        v-if="education.startDate != 'Invalid date' && education.endDate != 'Invalid date'"
        icon="bx-calendar"
      >
        {{year(education.startDate)}} — {{year(education.endDate)}}
      </IconLabel>
    </div>
  </div>
</template>

<script>
import * as datefns from 'date-fns';

export default {
  props: {
    education: Object
  },
  methods: {
    year(date) {
      return datefns.getYear(new Date(date))
    }
  },
  computed: {
    degree() {
      const items = [];
      if (this.education.degreeName) items.push(this.education.degreeName);
      if (this.education.fieldOfStudy) items.push(this.education.fieldOfStudy);
      return items.join(', ')
    }
  }
}
</script>

<style lang="scss" scoped>
h1 {
  font-weight: 500;
  font-size: 1.15rem;
}
.education-item {
  margin-top: 20px;
}
</style>
