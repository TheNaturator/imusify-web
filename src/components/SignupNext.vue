<template>
  <section class="signupnext">
    <div class="body">
      <h1 class="heading">{{$t('signUpNextCompleteRegistration')}} {{credentials.email}}</h1>
      <p class="subheading">{{$t('signUpNextCompleteRegistrationSubheader')}}
      </p>
      <form @submit.prevent="onSubmit()">
        <div class="form-group">
          <label class="control-label">{{$t('emailAddress')}}</label>
          <input type="text"
                 id="username"
                 placeholder="example@email.com"
                 class="form-control"
                 v-model="credentials.username">
        </div>
        <div class="form-group">
          <label class="control-label">{{$t('password')}}</label>
          <input type="text"
                 id="password"
                 :placeholder="$t('passwordPlaceholder')"
                 class="form-control"
                 v-model="credentials.password">
        </div>
        <div class="form-group">
          <label class="control-label">{{$t('passwordRepeat')}}</label>
          <input type="text"
                 id="passwordConfirm"
                 :placeholder="$t('passwordRepeatPlaceholder')"
                 class="form-control"
                 v-model="credentials.confirmPassword">
        </div>
        <div class="form-group">
          <div class="checkbox long-text">
            <label>
              <input class="checkbox" type="checkbox"/>
              <span></span>{{$t('signUpNextTermsOfUse')}}</label>
          </div>
        </div>
        <div class="form-group">
          <div class="checkbox">
            <label>
              <input class="checkbox2" type="checkbox"/>
              <span></span>
              {{$t('signUpNextSubscribe')}}</label>
          </div>
        </div>
        <div class="cta left">
          <button class="subbutton">{{$t('signup')}}</button>
        </div>
      </form>
    </div>
  </section>
</template>
<script>
import moment from 'moment';
import { mapActions, mapGetters, mapMutations } from 'vuex';
import * as types from '../store/types';

export default {
  name: 'signupnext',
  data() {
    return {};
  },
  computed: {
    ...mapGetters({
      status: types.ACCOUNTS_LOGIN_STATUS,
      token: types.ACCOUNTS_TOKEN,
      credentials: types.ACCOUNTS_USER_CREDENTIALS,
    }),
  },
  methods: {
    ...mapActions({
      signup: types.ACCOUNTS_SIGNUP,
    }),
    ...mapMutations({
      status: types.ACCOUNTS_LOGIN_STATUS,
    }),
    onSubmit() {
      if (this.credentials.password !== this.credentials.confirmPassword) {
        this.status('Passwords do not match');
        return false;
      }

      delete this.credentials.confirmPassword;

      this.credentials.date_created = moment(new Date()).format('YYYY-MM-DD hh:mm:ss');
      this.credentials.date_of_birth = moment('1970-01-01').format('YYYY-MM-DD');

      return this.signup(this.credentials).then(() => {
        this.$router.push('/');
      });
    },
  },
};
</script>
<style lang="scss" scoped>
.signupnext {
  .body {
    max-width: 50rem !important;
    .heading {
      text-align: center;
      font-size: 4rem;
      margin-bottom: 4rem;
    }
    .subheading {
      text-align: center;
      margin-bottom: 4rem;
    }
    .long-text {
      margin-top: 4rem;
    }
    .cta {
      margin-top: 4rem;
    }
  }
  .subbutton {
    text-transform: uppercase;
  }
}
</style>
