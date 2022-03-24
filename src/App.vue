<template>
  <div class="container">
    <HeaderContainer v-bind:userList="userList" />
    <BodyContainer />
  </div>
</template>

<script>
import BodyContainer from "@/container/BodyContainer/BodyContainer.vue";
import HeaderContainer from "@/container/HeaderContainer/HeaderContainer.vue";
import axios from "axios";

import "@/App.css";

export default {
  name: "App",
  components: {
    HeaderContainer: HeaderContainer,
    BodyContainer: BodyContainer,
  },
  data() {
    return {
      user: {
        userList: [
          {
            id: 1,
            name: "Name 1",
            surname: "Surname 1",
            userName: "username1",
          },
          {
            id: 2,
            name: "Name 2",
            surname: "Surname 2",
            userName: "username2",
          },
          {
            id: 3,
            name: "Name 3",
            surname: "Surname 3",
            userName: "username3",
          },
          {
            id: 4,
            name: "Name 4",
            surname: "Surname 4",
            userName: "username4",
          },
          {
            id: 5,
            name: "Name 5",
            surname: "Surname 5",
            userName: "username5",
          },
        ],
        selectedUserId: "",
        deselectSelectedUserText: "Deselect User",
      },
    };
  },
  mounted() {
    console.log("created Çalıştı..");
    axios
      .get(
        "https://raw.githubusercontent.com/teyfikavkan/vue3-cdn-todolist/main/mock/userList.json"
      )
      .then((result) => {
        const user = {
          userList: result.data.userList,
        };
        this.user = { ...this.user, ...user };
      })
      .catch((error) => {
        console.error(error);
      });
  },
  methods: {
    onClickUserListDropdown(item) {
      this.selectedUserId = item.id;
      console.log(item);
    },
  },
  provide() {
    return {
      onClickUserListDropdown: this.onClickUserListDropdown,
      userList: this.user.userList,
      selectedUserId: this.selectedUserId,
    };
  },
};
</script>