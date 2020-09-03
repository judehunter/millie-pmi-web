<template>
  <main class="padded-container index-page">
    <div class="bg" />
    <template v-if="loading == 0">
      <h1 class="sign-up-title">
        Sign up to our PMI program!
      </h1>
      <form class="sign-up-form" autocomplete="off">
        <IconLabel icon="bxs-user-circle">
          Name
        </IconLabel>
        <TextInput :value.sync="form.name" />

        <IconLabel icon="bxs-envelope">
          Email
        </IconLabel>
        <TextInput :value.sync="form.email" />

        <IconLabel icon="bxl-linkedin-square">
          LinkedIn URL
        </IconLabel>
        <TextInput :value.sync="form.linkedInUrl" />

        <IconLabel icon="bxs-book">
          Areas of expertise
        </IconLabel>
        <TextInput :value.sync="form.expertise[0]" />
        <TextInput :value.sync="form.expertise[1]" />
        <TextInput :value.sync="form.expertise[2]" />

        <IconLabel icon="bxs-graduation">
          Undergraduate graduation year
        </IconLabel>
        <TextInput :value.sync="form.graduationYear" />

        <Checkbox :value.sync="form.internationalSchool" labeled>
          I went to an international high school
        </Checkbox>

        <IconLabel icon="bxs-wink-smile">
          Anything else?
        </IconLabel>
        <TextBox :value.sync="form.moreInfo" />

        <div class="submit-button">
          <PlainButton @click="submit">
            Submit!
          </PlainButton>
        </div>
      </form>
    </template>
    <template v-else-if="loading == 1">
      <div class="loading">
        We're fetching your LinkedIn profile.<br>
        <IconLabel icon="bx-loader-alt bx-spin" style="font-size: 5rem; margin: 30px 0;" />
      </div>
    </template>
    <template v-else-if="loading == 2">
      <div class="loading">
        All done! You can leave the page now.<br>
        <IconLabel icon="bx-check" style="font-size: 5rem; margin: 30px 0;" />
      </div>
    </template>
    <template v-else-if="loading == -1">
      <div class="loading">
        Whoops! Something went wrong!
        <IconLabel icon="bxs-error-circle" style="font-size: 5rem; margin: 30px 0;" />
      </div>
    </template>
  </main>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
        email: '',
        linkedInUrl: '',
        expertise: ['', '', ''],
        moreInfo: '',
        graduationYear: '',
        internationalSchool: false
      },
      loading: 0
    }
  },
  methods: {
    async submit() {
      this.loading = 1;
      try {
        await this.$axios.post('/', this.form);
        this.loading = 2;
      } catch (err) {
        this.loading = -1;
      }
    }
  }
}
</script>

<style lang="scss" scoped>
h1 {
  font-size: 2rem;
  font-weight: bold;
  // margin: .3em 0;
}
h2 {
  font-size: 1.4rem;
  font-weight: bold;
  // margin: .3em 0;
}
.bg {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: $primary;
  z-index: -1;
}
.sign-up-title {
  text-align: center;
}
.sign-up-form {
  max-width: 400px;
  margin: 20px auto 30px;
  padding: 20px;
  border-radius: 5px;
  background-color: white;
  color: black;
  box-shadow: 0 1px 1px rgba(16,27,30,0.15), 0 2px 2px rgba(16,27,30,0.15), 0 4px 4px rgba(16,27,30,0.15), 0 8px 8px rgba(16,27,30,0.15), 0 16px 16px rgba(16,27,30,0.15);
  display: flex;
  flex-direction: column;
}
.index-page {
  color: white;
}

.i-went {
  @include flex-center(v);

  span {
    flex-grow: 1;
  }
}

.submit-button {
  text-align: right;
  margin-top: 20px;
  margin-bottom: -30px;

  button {
    box-shadow: 0 1px 1px rgba(16,27,30,0.15), 0 2px 2px rgba(16,27,30,0.15), 0 4px 4px rgba(16,27,30,0.15), 0 8px 8px rgba(16,27,30,0.15), 0 16px 16px rgba(16,27,30,0.15);
  }
}

.loading {
  @include flex-center(vh);
  flex-direction: column;
  max-width: 500px;
  margin: 0 auto;
  padding: 20px;
}

::v-deep input, textarea {
  margin-top: 10px;
  // margin-bottom: 10px;
}

::v-deep input + .icon-label, textarea + .icon-label {
  margin-top: 25px;
}

::v-deep .checkbox {
  margin-top: 25px;
  margin-bottom: 25px;
}
</style>
