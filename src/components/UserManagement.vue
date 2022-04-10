<script>
export default {
  props: ["data", "newUser"],
  emits: ["show-users", "add-user"],
  methods: {
    showUsers: function () {
      this.$emit("show-users");
    },

    showAddUserDialog: function () {
      const addUserDialogModal = new bootstrap.Modal(
        document.getElementById("addUserDialog"),
        {
          keyboard: false,
        }
      );
      addUserDialogModal.toggle();
    },

    addUser: function () {
      this.newUser._id = this.generateUserId();
      this.newUser.index = this.data[this.data.length -1].index + 1
      if (
        this.newUser.name != "" &&
        this.newUser.company != "" &&
        this.newUser.salary != ""
      )
        this.$emit("add-user", this.newUser);
    },

    addName: function (event) {
      this.newUser.name = event.target.value;
    },

    addCompany: function (event) {
      this.newUser.company = event.target.value;
    },

    addSalary: function (event) {
      this.newUser.salary = event.target.value;
    },

    generateUserId: function () {
      let timestamp = ((new Date().getTime() / 1000) | 0).toString(16);
      return (
        timestamp +
        "xxxxxxxxxxxxxxxx"
          .replace(/[x]/g, function () {
            return ((Math.random() * 16) | 0).toString(16);
          })
          .toLowerCase()
      );
    },
  },
};
</script>

<template>
  <div class="card">
    <div class="card-body">
      <h5 class="card-title">User Management</h5>
      <button type="button" class="btn btn-success" @click="showUsers()">
        Show All Users
      </button>
      <button
        type="button"
        class="btn btn-primary"
        @click="showAddUserDialog()"
      >
        Add a User
      </button>
    </div>
  </div>

  <div
    class="modal fade"
    id="addUserDialog"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Add a User</h5>
          <button
            type="button"
            class="btn-close"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>
        <div class="modal-body">
          <form>
            <div class="form-group row">
              <label for="username-add" class="col-sm-2 col-form-label"
                >Name</label
              >
              <div class="col-sm-10">
                <input
                  type="text"
                  class="form-control"
                  id="username-add"
                  value=""
                  @blur="addName($event)"
                />
              </div>
            </div>
            <div class="form-group row">
              <label for="company-add" class="col-sm-2 col-form-label"
                >Company</label
              >
              <div class="col-sm-10">
                <input
                  type="text"
                  class="form-control"
                  id="company-add"
                  value=""
                  @blur="addCompany($event)"
                />
              </div>
            </div>
            <div class="form-group row">
              <label for="salary-add" class="col-sm-2 col-form-label"
                >Salary</label
              >
              <div class="col-sm-10">
                <input
                  type="text"
                  class="form-control"
                  id="salary-add"
                  value=""
                  @blur="addSalary($event)"
                />
              </div>
            </div>
          </form>
        </div>
        <div class="modal-footer">
          <button
            type="button"
            class="btn btn-secondary"
            data-bs-dismiss="modal"
          >
            Close
          </button>
          <button type="button" class="btn btn-primary" @click="addUser()">
            Add
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
button {
  margin-right: 10px;
}
.card {
  margin-top: 10px;
}
</style>
