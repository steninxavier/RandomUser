<template>
  <div class="main">
    <div class="heading">
      <h2>RANDOM USER PALLET</h2>
      <hr />
    </div>
    <div class="container">
      <div class="image">
        <img :src="picture" />
      </div>
      <el-button round @click="reloadPage"><b>Next Profile</b></el-button>
      <el-tabs type="border-card" class="demo-tabs">
        <el-tab-pane label="Full Name">{{ title }}. {{ firstname }} {{ lastname }}</el-tab-pane>
        <el-tab-pane label="Email">{{ email }}</el-tab-pane>
        <el-tab-pane label="Age">{{ age }}</el-tab-pane>
        <el-tab-pane label="Address">{{ location }} {{ locationName }} {{ country }}</el-tab-pane>
        <el-tab-pane label="Phone">{{ phone }}</el-tab-pane>
        <el-tab-pane label="Password">{{ password }}</el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import axios from "axios";
export default defineComponent({
  methods: {
    reloadPage() {
      window.location.reload();
    },
  },
  name: "RandomUser",
  data() {
    return {
      title: [],
      firstname: [],
      lastname: [],
      age: [],
      email: [],
      location: [],
      locationName: [],
      country: [],
      phone: [],
      password: [],
      picture: [],
    };
  },
  mounted() {
    axios.get("https://randomuser.me/api/").then((data) => {
      this.title = data.data.results[0].name.title;
      this.firstname = data.data.results[0].name.first;
      this.lastname = data.data.results[0].name.last;
      this.age = data.data.results[0].dob.age;
      this.email = data.data.results[0].email;
      this.location = data.data.results[0].location.street.number;
      this.locationName = data.data.results[0].location.street.name;
      this.country = data.data.results[0].location.country;
      this.phone = data.data.results[0].cell;
      this.password = data.data.results[0].login.password;
      this.picture = data.data.results[0].picture.large
    });
  },
});
</script>
<style>
.demo-tabs > .el-tabs__content {
  padding: 50px;
  background-color: #f4f5f7;
  color: #6b778c;
  font-size: 32px;
  font-weight: 600;
  font-family: "Open Sans", sans-serif;
}
.demo-tabs {
  margin: 20px 0px 0px 430px;
  align-items: center;
  width: 519px;
  font-family: "Open Sans", sans-serif;
}
img {
  border-radius: 50%;
  border: 1px solid #808080;
  padding: 10px;
  height: 140px;
  width: 140px;
}
hr {
  width: 200px;
  margin-bottom: 15px;
}
.container {
  border: 2px solid #3db2ff;
  padding: 40px 0px 40px 0px;
  background-color: whitesmoke;
}
.heading {
  color: #3db2ff;
  font-weight: 600;
  font-family: "Lato", sans-serif;
}
@media only screen and (max-width: 600px) {
  .demo-tabs {
    margin: 0px;
    width: 290px;
  }
  .main {
    width: 300px;
  }
}
</style>
