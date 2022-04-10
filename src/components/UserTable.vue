<template>
  <table class="table" id="userTable">
    <thead>
      <tr>
        <th scope="col">Index</th>
        <th scope="col">Name</th>
        <th scope="col">isActive</th>
        <th scope="col">Salary</th>
        <th scope="col">Company</th>
        <th scope="col">Operations</th>
      </tr>
    </thead>
    <tbody id="userTableBody">
      <User
        :key="user._id"
        v-for="user in show"
        :user="user"
        :editForm="editForm"
        @user-del="$emit('user-del', $event)"
        @user-update="$emit('user-update', $event)"
      />
    </tbody>
  </table>
</template>
<script>
import User from "./User.vue";

export default {
  props: ["show", "editForm"],
  components: {
    User,
  },
};
</script>

<style scoped></style>
