<template>
  <div class="input-group mb-2">
      {{"selectedUserId" + selectedUserId}}
    <div class="input-group-prepend" style="margin-right: 5px">
      <div v-if="isThereAnyUser()" style="background-color: white">
        <button
          class="btn btn-outline-secondary dropdown-toggle"
          type="button"
          data-toggle="dropdown"
          aria-haspopup="true"
          aria-expanded="false"
          data-allow-clear="true"
        >
          {{ getSelectedUserName }}
          <span
            class="close bs-select-clear-selected"
            :class="{
              deselectUser: selectedUserId && selectedUserId !== '',
            }"
            :title="deselectSelectedUserText"
            v-show="selectedUserId && selectedUserId !== ''"
            @click="onDeselectSelectedUser($event)"
          >
            <span style="font-size: small">X</span>
          </span>
        </button>
        <div v-if="checkUser">
          <div class="dropdown-menu">
            <div v-for="subUser in this.userList" :key="subUser.id">
              <button
                class="dropdown-item"
                @click="onClickUserListDropdown(subUser)"
              >
                {{ subUser.userName }}
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
    <input
      type="text"
      class="form-control"
      style="margin-right: 5px"
      :placeholder="task.taskDescriptionPlaceHolder"
      @input="onChangeTaskEvent"
      v-bind:value="task.taskDescription"
    />
    <button type="button" class="btn btn-primary" v-on:click="onAddTaskEvent">
      {{ task.addTaskText }}
    </button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userListText: "User List",
      deselectSelectedUserText: "Deselect User",

      task: {
        addTaskText: "Add Task",
        taskDescriptionPlaceHolder: "Task Description",
        taskDescription: "",
      },
    };
  },
  computed: {
    getSelectedUserName() {
      if (this.selectedUserId && this.selectedUserId !== "") {
        return this.userList.find((u) => u.id === this.selectedUserId).userName;
      }

      return this.userListText;
    },
  },
  methods: {
    checkUser() {
      console.log(this.userList);
      return Array.isArray(this.userList) && this.userList.length !== 0;
    },
    isThereAnyUser() {
      return this.userList.length !== 0;
    },
    onChangeTaskEvent: function (event) {
      this.task.taskDescription = event.target.value;
    },
    onAddTaskEvent() {
      if (this.task.taskDescription && this.task.taskDescription !== "") {
        if (!this.selectedUserId || this.selectedUserId === "") {
          alert("You must choose a user!");
        } else {
          this.task.taskList.push({
            isDone: false,
            taskDescription: this.task.taskDescription,
            userId: this.selectedUserId,
          });
          this.task.taskDescription = "";
        }
      } else {
        alert("Task description cannot be at the moment.");
      }
    },
  },
  inject: {
    onClickUserListDropdown: "onClickUserListDropdown",
    selectedUserId: "selectedUserId",
    userList: "userList",
  },
};
</script>