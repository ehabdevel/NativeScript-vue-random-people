<template>
  <Page loaded="onPageLoaded">
    <ActionBar title="Random People"/>
    <ScrollView>
      <StackLayout class="home-panel">
        <ListView class="list-group" for="user in users" style="height:1250px">
          <v-template>
            <GridLayout columns="auto, *" rows="*, *" class="list-group-item">
              <Image
                col="0"
                row="0"
                rowspan="2"
                :src="user.picture.medium"
                class="thumb img-circle"
              />
              <Label
                col="1"
                row="0"
                :text="`${user.name.title}: ${user.name.first} ${user.name.last}`"
                class="list-group-item-heading"
                @tap="onUserItemTap(user)"
              />
              <label col="1" row="0" :text="user.email" class="item-details"/>
            </GridLayout>
          </v-template>
        </ListView>
      </StackLayout>
    </ScrollView>
  </Page>
</template>

<script>
import * as http from "http";
export default {
  methods: {
    onUserItemTap(user) {
      console.log("User with first name: " + user.name.first + " tapped");
    }
  },
  data() {
    return {
      users: []
    };
  },
  mounted() {
    http.getJSON("https://randomuser.me/api/?results=30").then(
      result => {
        this.users = result.results;
      },
      error => {
        console.log(error);
      }
    );
  }
};
</script>

<style scoped>
ActionBar {
  background-color: #2553ff;
  color: #ffffff;
}

.img-circle {
  width: 55;
  height: 55;
  margin: 5;
  border-radius: 50%;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.1);
}

.list-group-item-heading {
  font-size: 15;
  text-transform: capitalize;
  color: #4b4b4b;
  vertical-align: middle;
}

.item-details {
  font-size: 13;
  padding-bottom: 5;
  opacity: 0.8;
  color: #a8a689;
  vertical-align: bottom;
}
</style>
