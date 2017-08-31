<template>
  <v-app light>
    <v-layout>
      <v-flex class="mb-3" xs12 md10 offset-md1>
        <v-card>
          <wog-header :editable="editable" @drawerChanged="drawerChanged" @tabChange="tabChange"></wog-header>
          <wog-content :editable="editable" :drawer="drawer" :page="tab"></wog-content>
          <wog-footer></wog-footer>
        </v-card>
      </v-flex>
    </v-layout>
  </v-app>
</template>

<script>
  import * as FB from 'firebase'

  export default {
    created() {
      var self = this;
      FB.auth().onAuthStateChanged(function(user) {
        if (user) {
          self.editable = true;
        }
        else {
          self.editable = false;
        }
      });
    },
    data () {
      return {
        drawer: false,
        editable: false,
        tab: null
      }
    },
    methods: {
      drawerChanged: function(val) {
        this.drawer = val;
      },
      tabChange: function(val) {
        this.tab = val;
        setTimeout(function() {this.tab=null}, 100)
      }
    }
  }
</script>

<style lang="stylus">
  @import './stylus/main'
</style>
