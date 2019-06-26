<template>
  <div>
    <div class="card">
      <div class="card-body">
        <div class="row">
          <div class="col-md-1">
            <button class="btn btn-outline-secondary btn-sm" v-on:click="showmenu=!showmenu">
              <i class="material-icons">menu</i>
            </button>
          </div>
          <div class="col-md-4">
            <h3>Contact information system</h3>
          </div>
          <div class="col-md-4">
            <h3>Version 9.0.0</h3>
          </div>
        </div>
      </div>
    </div>

    <!-- main menu section -->

    <div class="row">
      <div class="col-md-2" v-if="showmenu">
        <div class="card" style="background-color: #f5f5f5;">
          <div class="card-body">
            <a v-on:click="showcont=!showcont">
              <i class="fa fa-folder"></i>
              &nbsp;&nbsp;Contacts
            </a>
            <br>
            <div v-if="showcont">
              <a v-on:click="selectcont()">
                <i class="fa fa-wrench"></i>
                &nbsp;&nbsp;Contact View
              </a>
              <br>
              <div>
                <a v-for="item in contlist" :key="item.id" v-on:click="cont=item" class="NFM">
                  <span v-bind:class="{ red : item.id == cont.id }">
                    <i class="fa fa-star"></i>
                    &nbsp;&nbsp;{{ item.name }}
                    <br>
                  </span>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!--  main content -->
      
      <div class="col-md-10 card" style="overflow:auto; background-color: #f5f5f5;">
        <div v-if="mainview=='cont'">
          <div id="contact">
            <contact></contact>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import contact from "./contact.vue";

export default {
  name: "mainmenu",
  components: {
    contact
  },
  data: function() {
    return {
      cont: 0,
      showmenu: true,
      showcont: false,
      mainview: "none",
      contlist: []
    };
  },
  created: function() {
    this.refreshcontacts();
  },
  methods: {
    refreshcontacts: function() {
      axios
        .get("/contacts/test")
        .then(
          result => (this.contlist = result.data),
          result => alert("Test status " + result.status)
        );
    },
    selectcont: function() {
      this.mainview = "cont";
    }
  },
  props: {
    msg: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->

<style scoped>
a {
  color: #42b983;
}
</style>
