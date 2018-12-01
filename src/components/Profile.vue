<template>
  <section class="profile">
    <div class="body">
      <h1 class="heading">{{$t('profileCompleteYourProfile')}}</h1>
      <div class="two-column">
        <div class="left-sec">
          <img src="../assets/logo.png" />
          <button class="uploadbutton">
            <span class="icon-svg upload">
              <icon name="imageUpload" />
            </span>
            {{$t('profileUploadImage')}}
          </button>
        </div>
        <div class="right-sec">
          <form @submit.prevent="onUpdateAccount">
            <div class="form-group">
              <label class="control-label">{{$t('profileFirstName')}}</label>
              <input type="text"
                     class="form-control"
                     v-model="user.first_name"
                     :placeholder="$t('profileFirstNamePlaceholder')">
            </div>
            <div class="form-group">
              <label class="control-label">{{$t('profileLastName')}}</label>
              <input type="text"
                     class="form-control"
                     v-model="user.last_name"
                     :placeholder="$t('profileLastNamePlaceholder')">
            </div>
            <div class="form-group">
              <label class="control-label">{{$t('profileWalletAddress')}}</label>
              <input type="text"
                     class="form-control"
                     v-model="user.wallet_address"
                     :placeholder="$t('profileWalletAddressPlaceholder')">
            </div>
            <div class="form-group">
              <label class="control-label">{{$t('profileDateOfBirth')}}</label>
              <input type="text"
                     class="form-control"
                     v-model="user.date_of_birth"
                     :placeholder="$t('profileDateOfBirthPlaceholder')">
            </div>
            <div class="form-group">
              <label class="control-label">{{$t('profileBiography')}}</label>
              <textarea id="biography"
                        class="form-control"
                        v-model="user.bio"
                        :placeholder="$t('profileBiographyPlaceholder')"
                        style="resize:none"></textarea>
            </div>
            <div class="form-group">
              <label class="control-label">{{$t('profileGender')}}</label>
              <select class="form-control" v-model="user.gender">
                <option value="" selected>{{$t('profileSelectGender')}}</option>
                <option value="M">{{$t('male')}}</option>
                <option value="F">{{$t('female')}}</option>
                <option value="U">{{$t('profileDeclineToState')}}</option>
              </select>
            </div>
            <div class="cta left">
              <button class="savebutton">{{$t('profileSaveSettings')}}</button>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>
<script>
import { mapActions, mapGetters } from 'vuex';
import Icon from '@/components/Icon.vue';
import * as types from '../store/types';

export default {
  name: 'profile',
  components: {
    Icon,
  },
  data() {
    return {
    };
  },
  computed: {
    ...mapGetters({
      status: types.ACCOUNTS_LOGIN_STATUS,
      credentials: types.ACCOUNTS_USER_CREDENTIALS,
      user: types.ACCOUNTS_USER,
    }),
  },
  methods: {
    ...mapActions({
      updateAccount: types.ACCOUNTS_USER_UPDATE,
    }),
    onUpdateAccount() {
      this.updateAccount(this.user)
        .finally(() => {
          this.$router.push('/');
        });
    },
  },
};
</script>
<style lang="scss" scoped>
  .profile {
    .body {
      .heading {
        text-align: center;
        font-size: 5rem;
        font-weight: 300;
        font-style: normal;
      }
      .two-column {
        align-items: flex-start;
        margin-top: 4rem;
        .left-sec {
          margin-top: 2rem;
          width: 20rem;
        }
        button {
          border: none;
        }
      }
    }
    .savebutton {
      text-transform: uppercase;
    }
  }
</style>
