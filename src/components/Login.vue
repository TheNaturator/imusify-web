<template>
  <section class="login modal">
    <a href="" @click.prevent="toggleLoginOpen" class="close">
      <Icon name="close" />
    </a>
    <div class="body">
      <h1 class="heading">{{$t('signInToImusify')}}</h1>
      <p class="subheading">{{$t('signIntoImusifySubHeader')}}
      </p>
      <social-icons v-if="false"></social-icons>
      <div class="or-ui" v-if="false"><span>OR</span></div>
      <div>
        <form @submit.prevent="onSubmit()">
          <div class="form-group">
            <label class="control-label">{{$t('emailAddress')}}</label>
            <input type="text" id="email" class="form-control"
              :placeholder="$t('emailAddressPlaceholder')" v-model="credentials.email">
          </div>
          <div class="form-group">
            <label class="control-label">{{$t('password')}}</label>
            <input type="password" id="password" class="form-control"
              :placeholder="$t('passwordPlaceholder')" v-model="credentials.password">
          </div>
          <div class="form-group">
            <div class="checkbox">
              <label><input type="checkbox"/> <span></span> {{$t('loginKeepMeSignedIn')}}</label>
            </div>
          </div>
          <div class="cta dubble">
            <button>{{$t('login')}}</button>
            <button type="button"
                    @click="openSignupModal()">{{$t('signup')}}</button>
          </div>
        </form>
      </div>
      <div class="status" v-if="status">
        {{status}}
      </div>
    </div>
  </section>
</template>

<script>
import Icon from '@/components/Icon.vue';
import SocialIcons from '@/components/SocialIcons.vue';
import { mapActions, mapMutations } from 'vuex';
import * as types from '../store/types';

export default {
  name: 'login',
  components: {
    Icon,
    SocialIcons,
  },
  data() {
    return {
      credentials: {
        email: '',
        password: '',
      },
      status: '',
    };
  },

  methods: {
    ...mapActions({
      login: types.ACCOUNTS_USER,
    }),

    ...mapMutations({
      isLoginOpen: types.TOGGLER_LOGIN,
      isSignupOpen: types.TOGGLER_SIGNUP,
    }),

    onSubmit() {
      this.login(this.credentials).then(() => {
        this.$router.replace(this.$route.query.redirect || '/');
      });
    },

    openSignupModal() {
      this.isLoginOpen(false);
      this.isSignupOpen(true);
    },

    signupPage() {
      this.$router.push('/signupnext');
    },

    toggleLoginOpen() {
      this.$emit('toggleLoginOpen', false);
    },
  },
};
</script>
<style lang="scss" scoped>
@import "./src/assets/styles/base.scss";

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
  .cta {
    margin-top: 4rem;
  }
  button {
    padding: 0;
  }
}
</style>
