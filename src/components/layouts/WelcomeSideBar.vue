<template>

  <v-navigation-drawer
    v-model="show"
    app
    temporary
    dark
    src="@/assets/img/bgDownload.jpg"
  >

    <v-list>
      <v-list-item>
          <v-img src="@/assets/logo.svg" max-width="190" />
      </v-list-item>
    </v-list> <!-- BUSINESS LOGO AND SUBTITLE -->

    <v-divider />

    <v-list class="mt-2">
      <v-list-item
        v-for="([text, link], i) in items"
        :key="i"
        link
        @click="text === 'Contact' ? dialog = true  : $vuetify.goTo(link)"
      >
        <v-list-item-content>
          <v-list-item-title class="subtitile-1 text-center">{{ text }}</v-list-item-title>
        </v-list-item-content>
      </v-list-item>
      <v-list-item>
        <v-btn depressed text block large @click="signInDialog = true">
          <span class="text-capitalize">Log In</span>
        </v-btn>
      </v-list-item>
        <v-list-item>
          <v-btn depressed color="primary" block large @click="signUpDialog = true">
            <span class="text-capitalize">Sign Up</span>
          </v-btn>
      </v-list-item>
    </v-list> <!-- SIDE NAVIGATION LINKS -->

    <contact-modal 
      :visible="dialog"
      @close="dialog = false"
    /> <!-- CONTACT FORM MODAL -->

    <sign-in-modal
      :visible="signInDialog"
      @close="signInDialog = false"
    />  <!-- SIGN IN AUTH MODAL -->

     <sign-up-modal
      :visible="signUpDialog"
      @close="signUpDialog = false"
    />  <!-- SING UP AUTH MODAL -->

  </v-navigation-drawer> <!-- NAVIGATION DRAWER -->

</template>

<script>
  export default {
    name: 'home-side-bar',

    data () {
      return {
        dialog: false,
        signInDialog: false,
        signUpDialog: false
      }
    },

    components: {
      ContactModal: () => import('@/components/pages/modals/ContactModal'),
      SignInModal: () => import('@/components/pages/modals/SignInModal'),
      SignUpModal: () => import('@/components/pages/modals/SignUpModal')
    },
    
    props: ['items', 'visible'],

    computed: {
        show: {
            get () {
                return this.visible
            },
            set (value) {
                if (!value) {
                    this.$emit('close')
                }
            }
        }
    }
  }
</script>