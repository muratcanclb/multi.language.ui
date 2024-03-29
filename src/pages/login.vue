<script>
import AuthProvider from '@/views/pages/authentication/AuthProvider.vue'
import { useGenerateImageVariant } from '@core/composable/useGenerateImageVariant'
import { VNodeRenderer } from '@layouts/components/VNodeRenderer'
import { themeConfig } from '@themeConfig'
import { emailValidator, requiredValidator } from '@validators'

import authV2LoginIllustrationBorderedDark from '@images/pages/auth-v2-login-illustration-bordered-dark.png'
import authV2LoginIllustrationBorderedLight from '@images/pages/auth-v2-login-illustration-bordered-light.png'
import authV2LoginIllustrationDark from '@images/pages/auth-v2-login-illustration-dark.png'
import authV2LoginIllustrationLight from '@images/pages/auth-v2-login-illustration-light.png'
import authV2MaskDark from '@images/pages/misc-mask-dark.png'
import authV2MaskLight from '@images/pages/misc-mask-light.png'
import i18n from '@/plugins/i18n';

export default {
  name: "LocaleSwitcher",
  data() {
    return {
      locales2: ["ar", "tr", "en", "fr"],
      
      authThemeImg: useGenerateImageVariant(authV2LoginIllustrationLight, authV2LoginIllustrationDark, authV2LoginIllustrationBorderedLight, authV2LoginIllustrationBorderedDark, true),
      //authThemeMask : useGenerateImageVariant(authV2MaskLight, authV2MaskDark),
      isPasswordVisible: false,
      email: "",
      password: "",
      rememberMe: false,
      locales: [{ value: "ar", key: "Arapça" }, { value: "tr", key: "Türkçe" }, { value: "en", key: "İngilizce" }, { value: "fr", key: "Fransızca" }],
    };
  },
  methods: {
    updateLanguage() {
      sessionStorage.setItem("locale", this.$i18n.locale);
    },
  },
  mounted() {
    console.log(sessionStorage.getItem("locale"),"language")
    if (sessionStorage.getItem("locale")) {
      this.$i18n.locale = sessionStorage.getItem("locale");
    } else {
      sessionStorage.setItem("locale", this.$i18n.locale);
    }
  },
};
</script>
<template>
  <VRow no-gutters class="auth-wrapper">
    <VCol lg="8" class="d-none d-lg-flex">
      <div class="position-relative auth-bg rounded-lg w-100 ma-8 me-0">
        <div class="d-flex align-center justify-center w-100 h-100">
          <VImg max-width="505" :src="authThemeImg" class="auth-illustration mt-16 mb-2" />
        </div>

        <VImg :src="authThemeMask" class="auth-footer-mask" />
      </div>
    </VCol>

    <VCol cols="12" lg="4" class="d-flex align-center justify-center">
      <VCard flat :max-width="500" class="mt-12 mt-sm-0 pa-4">
        <div style="margin: 0px 10px 5px 200px;" class="custom-select">
          <select :change="updateLanguage()" v-model="$i18n.locale"
            class="block w-full py-2 pl-3 pr-10 text-base border-gray-300 focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 sm:text-sm rounded-md">
            <option v-for="(locale, i) in locales" :key="locale.key" :value="locale.value">
              {{ locale.key }}
            </option>
          </select>
        </div>
        <VCardText>
          <VNodeRenderer class="mb-6" />

          <h5 class="text-h5 font-weight-semibold mb-1">
            {{ $t('Welcome') }} 👋🏻
          </h5>
        </VCardText>
        <VCardText>
          <VForm @submit.prevent="() => { }">
            <VRow>
              <!-- email -->
              <VCol cols="12">
                <VTextField v-model="email" :label="$t('Email')" type="email"
                  :rules="[requiredValidator, emailValidator]" />
              </VCol>

              <!-- password -->
              <VCol cols="12">
                <VTextField v-model="password" :label="$t('Password')" :rules="[requiredValidator]"
                  :type="isPasswordVisible ? 'text' : 'password'"
                  :append-inner-icon="isPasswordVisible ? 'tabler-eye-off' : 'tabler-eye'"
                  @click:append-inner="isPasswordVisible = !isPasswordVisible" />

                <div class="d-flex align-center flex-wrap justify-space-between mt-2 mb-4">
                  <VCheckbox v-model="rememberMe" :label="$t('Remember Me')" />
                  <a class="text-primary ms-2 mb-1" href="#">
                    {{ $t('Forgot Password') }}
                  </a>
                </div>
                <VBtn block type="submit">
                  {{ $t('Login') }}
                </VBtn>
              </VCol>

              <!-- create account -->
              <VCol cols="12" class="text-center">
                <a class="text-primary ms-2" href="#">
                  {{ $t('Create an account') }}
                </a>
              </VCol>
              <!-- auth providers -->
              <VCol cols="12" class="text-center">
                <AuthProvider />
              </VCol>
            </VRow>
          </VForm>
        </VCardText>
      </VCard>
    </VCol>
  </VRow>
</template>

<style lang="scss" scoped>
@use "@core/scss/template/pages/page-auth.scss";
.custom-select {
  position: relative;
  width: 200px;
}

.custom-select select {
  display: block;
  width: 100%;
  padding: 10px;
  font-size: 16px;
  font-family: Arial, sans-serif;
  color: #333;
  border: 1px solid #ccc;
  border-radius: 5px;
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  background-color: #fff;
  cursor: pointer;
}

.custom-select select:focus {
  outline: none;
  border-color: #007bff;
}

.custom-select::after {
  content: '\25BC';
  position: absolute;
  top: 50%;
  right: 10px;
  transform: translateY(-50%);
  pointer-events: none;
}
</style>

<route lang="yaml">
meta:
  layout: blank
  action: read
  subject: Auth
  redirectIfLoggedIn: true
</route>
