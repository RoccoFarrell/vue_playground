<template>
  <v-app light>
    <v-toolbar></v-toolbar>
    <main>
      <v-container fluid>
        <router-view>
          <v-layout class="ma-3">
            <v-flex xs4>
              <div>
                <v-btn light @click="add(1)" @dblclick="add(10)">Add</v-btn>
              </div>
              <div>
                <v-btn light @click="subtract(1)" @dblclick="subtract(10)">Subtract</v-btn>
              </div>
              <div>
                <v-btn light @click="error = !error">Error</v-btn>
              </div>
            </v-flex>
            <v-flex xs4>
              <h1>{{ age }}</h1>
            </v-flex>
            <v-layout v-if="error" xs4 justify-space-around>
              <v-icon large class="blue--text text--darken-2">mdi-anchor</v-icon>
            </v-layout>
            <!--
            <v-flex xs12>
              <h1>{{ mouse_event }}</h1>
            </v-flex>
          -->
          </v-layout>
          <v-layout>
            <v-flex xs12>
              <v-form v-model="test" ref="form1">
                <v-text-field
                  label="Name"
                  v-model="name"
                  required
                ></v-text-field>
              </v-form>
            </v-flex>
          </v-layout>
          <v-layout>
            <v-flex xs12 class="ma-3">
              <h1>{{ addToName() }}</h1>
            </v-flex>
          </v-layout>
          <v-form v-model="valid" ref="form">
          <v-expansion-panel>
            <v-expansion-panel-content key="1">
              <div slot="header">Item</div>
              <v-card>
                <v-card-text class="grey lighten-3">Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.</v-card-text>
              </v-card>
            </v-expansion-panel-content>
            <v-expansion-panel-content key="2">
              <div slot="header">Item</div>
              <v-card class="pa-3">
                  <v-text-field
                    label="Name"
                    v-model="name"
                    :rules="nameRules"
                    :counter="10"
                    required
                  ></v-text-field>
                  <v-text-field
                    label="E-mail"
                    v-model="email"
                    :rules="emailRules"
                    required
                  ></v-text-field>
                  <v-select
                    label="Item"
                    v-model="select"
                    :items="items"
                    :rules="[(v) => !!v || 'Item is required']"
                    required
                  ></v-select>
                  <v-checkbox
                    label="New"
                    v-model="checkbox"
                    :rules="[(v) => !!v || 'You must agree to continue!']"
                    required
                  ></v-checkbox>
                  <v-checkbox
                    label="Update"
                    v-model="checkbox"
                    :rules="[(v) => !!v || 'You must agree to continue!']"
                    required
                  ></v-checkbox>

                  <v-btn @click="submit" :class="{ green: valid, red: !valid }">submit</v-btn>
                  <v-btn @click="clear">clear</v-btn>
              </v-card>
            </v-expansion-panel-content>
          </v-expansion-panel>
          </v-form>
        </router-view>
      </v-container>
    </main>
    <v-footer></v-footer>
  </v-app>
</template>

<script>
  export default {
    data () {
      return {
        age: 25,
        mouse_event: {"event":"test"},
        name: "",
        valid: false,
        error: false,
        name: '',
        nameRules: [
          (v) => !!v || 'Name is required',
          (v) => v && v.length <= 10 || 'Name must be less than 10 characters'
        ],
        email: '',
        emailRules: [
          (v) => !!v || 'E-mail is required',
          (v) => /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
        ],
        select: null,
        items: [
          'Item 1',
          'Item 2',
          'Item 3',
          'Item 4'
        ],
        checkbox: false
      }
    },
    methods: {
      submit () {
        if (this.$refs.form.validate()) {
          this.$refs.form.$el.submit()
        }
      },
      clear () {
        this.$refs.form.reset()
      },
      add(inc){
        this.age += inc
      },
      subtract(dec){
        this.age -= dec
      },

      mouseEvent(event){
        console.log(event)
        this.mouse_event = event
      },

      addToName(){
        return "!!" + this.name + "!!"
      }
    }
}
</script>
