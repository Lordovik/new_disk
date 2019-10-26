<template>
  <v-app id="inspire">
    <v-content>
      <v-container
        class="fill-height"
        fluid
      >
        <v-row
          align="center"
          justify="center"
        >
          <v-col
            cols="12"
            sm="8"
            md="4"
          >
            <v-card class="elevation-12">
              <v-toolbar
                color="primary"
                dark
                flat
              >
                <v-toolbar-title>Вход</v-toolbar-title>
                <v-spacer></v-spacer>
                
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field
                    v-model="login"
                    label="Логин"
                    name="login"
                    prepend-icon="person"
                    type="text"
                    @keypress="checkEnter"
                  ></v-text-field>

                  <v-alert
                    border="bottom"
                    type="error"
                    colored-border
                    dense
                    v-if="errors.emptyLogin"
                  ><span style="color: red">Введите логин</span></v-alert>

                  <v-text-field
                    v-model="pass"
                    id="password"
                    label="Пароль"
                    name="password"
                    prepend-icon="lock"
                    type="password"
                  ></v-text-field>

                  <v-alert
                    border="bottom"
                    type="error"
                    :colored-border=true
                    dense
                    v-if="errors.emptyPass"
                  ><span style="color: red">Введите пароль</span></v-alert>

                  <v-alert
                    border="bottom"
                    type="error"
                    colored-border
                    dense
                    v-if="notMatching"
                  ><span style="color: red">Неправильный пароль или логин</span></v-alert>

                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="primary" @click="checkFields">Войти</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
  export default {
    props: {
      matched: Boolean
    },

    data() {
      return {
        login: '',
        pass: '',
        errors: {
          emptyLogin: false,
          emptyPass: false
        }
      };
    },

    computed: {
      notMatching(){
        return !this.hasErrors() && !this.matched;
      }
    },

    methods: {
      checkFields(){
        this.errors.emptyLogin = !this.login.length;
        this.errors.emptyPass = !this.pass.length;

        if(this.hasErrors()) return;

        this.$emit('dataValidated', this.login, this.pass);
      },

      hasErrors(){
        for(let error in this.errors){
          if(this.errors[error]) return true;
        }
        return false;
      },

      checkEnter(e){
        if(e.keyCode === 13) checkFields();
      }

    }

  }
</script>

<style>
@import 'https://fonts.googleapis.com/css?family=Roboto:300,400,500,700|Material+Icons';
</style>