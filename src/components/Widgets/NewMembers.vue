<template>
  <div>
    <app-section-loader :status="loader"></app-section-loader>
    <vue-perfect-scrollbar style="height:290px" :settings="settings">
      <v-list v-if="newMembers">
        <v-list-item class="listing" v-for="members in newMembers" avatar :key="members.id">
          <v-list-item-avatar>
            <img class="img-responsive" :src="members.photo_url" alt="user-image" />
          </v-list-item-avatar>
          <v-list-item-content>
            <span>{{members.customer_name}}</span>
          </v-list-item-content>
          <v-list-item-action>
            <v-flex>
              <v-btn fab dark small color="success" mr-2>
                <v-icon dark>ti-check</v-icon>
              </v-btn>
              <v-btn fab dark small color="error">
                <v-icon dark>ti-close</v-icon>
              </v-btn>
            </v-flex>
          </v-list-item-action>
        </v-list-item>
      </v-list>
    </vue-perfect-scrollbar>
  </div>
</template>

<script>
import api from "Api";

export default {
  data() {
    return {
      loader: false,
      newMembers: null,
      settings: {
        maxScrollbarLength: 100
      }
    };
  },
  mounted() {
    this.getMembers();
  },
  methods: {
    getMembers() {
      this.loader = true;
      const self = this;
      api
        .get("newCustomers.js")
        .then(response => {
          self.loader = false;
          this.newMembers = response.data;
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

