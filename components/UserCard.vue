<template>
  <div class="user-card">
    <!-- {{user}} -->
    <div class="user-card__avatar">
      <img :src="user.data.userProfile.photo || 'http://www.gravatar.com/avatar/?d=mp'" width="70" height="70">
    </div>
    <div class="user-card__info">
      <a :href="user.data.userProfile.url" target="_blank"><h1>{{user.name}}</h1></a>
      <h2 style="margin-bottom: 15px;">
        {{user.data.userProfile.title}}
      </h2>
      <IconLabel v-if="user.data.location" icon="bx-world">
        {{location}}
      </IconLabel>
      <IconLabel icon="bx-envelope">
        {{user.email}}
      </IconLabel>
      <IconLabel icon="bx-book">
        {{yrsOfExp}} year{{yrsOfExp == 1 || yrsOfExp == '&lt; 1' ? '': 's'}} of experience
      </IconLabel>

      <IconLabel v-if="user.data.formData.graduationYear" icon="bxs-graduation">
        undergrad in {{user.data.formData.graduationYear}}
      </IconLabel>

      <IconLabel v-if="user.data.formData.internationalSchool" icon="bx-globe">
        went to an international high school
      </IconLabel>

      <IconLabel icon="bx-bulb" style="margin-top: 15px;">
        areas of expertise:
      </IconLabel>
      {{user.data.formData.expertise.filter(x => x != '').join(', ')}}

      <template v-if="user.data.formData.moreInfo">
        <IconLabel icon="bx-info-circle" style="margin-top: 15px;">
          more info:
        </IconLabel>
        {{user.data.formData.moreInfo}}
      </template>

      <div class="user-card-education">
        <EducationItem v-for="(edu, idx) in (showAllEdu ? user.data.education : user.data.education.slice(0, 2))" :key="idx" :education="edu" />
      </div>

      <PlainButton v-if="user.data.education.length > 2 && !showAllEdu" style="margin-top: 15px;" @click="showAllEdu=true">
        see {{user.data.education.length - 2}} more
      </PlainButton>
    </div>
  </div>
</template>

<script>
import * as datefns from 'date-fns';
export default {
  props: {
    user: Object
  },
  data() {
    return {
      showAllEdu: false
    }
  },
  computed: {
    yrsOfExp() {
      const diff = datefns.differenceInYears(new Date(), new Date(this.user.data.education[0].endDate));
      return diff <= 0 ? '< 1' : diff;
    },
    location() {
      const items = [];
      if (this.user.data.userProfile.location.city) items.push(this.user.data.userProfile.location.city);
      if (this.user.data.userProfile.location.country) items.push(this.user.data.userProfile.location.country);
      return items.join(', ')
    }
  }
}
</script>

<style lang="scss" scoped>
h1 {
  font-weight: 600;
  font-size: 1.5rem;
  font-family: $display-stack;
  color: $primary;
}
.user-card {
  display: flex;

  & + & {
    margin-top: 30px;
  }

  &__avatar {
    margin-right: 20px;
    img {
      border-radius: 50%;
    }
  }
}
.user-card-education {
  // margin-left: -50px;
}
::v-deep .icon-label {
  margin: 3px 0;
}
</style>
