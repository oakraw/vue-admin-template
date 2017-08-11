<template>
<div class="fit-height">
<v-container class="center fit-height">
  <v-layout column wrap class="fit-width">
    <v-spacer></v-spacer>
    <v-flex xs12 sm6 offset-sm3 md4 offset-md4>
      <v-card>
        <v-card-title class="primary">
          <h3 class="white--text fit-width text-xs-center my-3">TITLE</h3>
        </v-card-title>
        <v-card-text>
          <v-container fluid>
            <v-text-field v-model="email" name="input-email" label="Email" type="email"></v-text-field>
            <v-text-field v-model="password" name="input-password" label="Password" hint="At least 8 characters" min="8" value="" type="password"></v-text-field>
            <!-- <div class="text-xs-center" v-if="loggingIn">
                  <v-progress-circular indeterminate v-bind:size="50" class="primary--text"></v-progress-circular>
                </div> -->
            <v-btn primary block dark @click.native="login">Login</v-btn>
          </v-container>

        </v-card-text>
      </v-card>
    </v-flex>
    <v-spacer></v-spacer>
  </v-layout>
  <progress-dialog ref="progressDialog" message="Logging in..."></progress-dialog>
</v-container>
</div>
</template>

<script>
import ProgressDialog from '@/components/common/ProgressDialog';

export default {
  components: {
    ProgressDialog,
  },
  data() {
    return {
      email: '',
      password: '',
    };
  },
  methods: {
    login(event) {
      event.preventDefault();
      event.stopPropagation();
      this.$refs.progressDialog.show();

      this.$auth.login().then(() => {
        this.$refs.progressDialog.hide();
        setTimeout(() => {
          this.$router.push({
            name: 'profile',
          });
        }, 100);
      });
    },
  },
};
</script>

<style lang="css" scoped>
.fit-height {
  height: 100%;
}
.fit-width{
  width: 100%;
}
</style>
