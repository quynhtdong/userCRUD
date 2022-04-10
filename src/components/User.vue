<template>
  <tr>
    <td>
      {{ user.index }}
    </td>
    <td>
      {{ user.name }}
    </td>
    <td>
      {{ user.isActive }}
    </td>
    <td>
      {{ user.salary }}
    </td>
    <td>
      {{ user.company }}
    </td>
    <td>
      <button
        type="button"
        class="btn btn-info"
        @click="showEditDialog(user._id)"
      >
        Edit
      </button>
      <button type="button" class="btn btn-danger" @click="del(user._id)">
        Delete
      </button>
    </td>
  </tr>
  <div
    class="modal fade"
    id="editUserDialog"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Edit a User</h5>
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
              <label for="username-edit" class="col-sm-2 col-form-label"
                >Name</label
              >
              <div class="col-sm-10">
                <input
                  type="text"
                  readonly
                  class="form-control-plaintext"
                  id="username-edit"
                  value=""
                />
              </div>
            </div>
            <div class="form-group row">
              <label for="salary-edit" class="col-sm-2 col-form-label"
                >Salary</label
              >
              <div class="col-sm-10">
                <input
                  type="text"
                  class="form-control"
                  id="salary-edit"
                  value=""
                  @blur="change($event)"
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
          <button type="button" class="btn btn-primary" @click="updateUser()">
            Save changes
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["user","editForm"],
  emits: ["user-del", "user-update"],
  methods: {
    del: function (userId) {
      this.$emit("user-del", userId);
    },
    showEditDialog: function (userId) {
      const editUserDialogModal = new bootstrap.Modal(
        document.getElementById("editUserDialog"),
        {
          keyboard: false,
        }
      );
      editUserDialogModal.toggle();
      document.getElementById('username-edit').value = this.user.name
      document.getElementById('salary-edit').value = this.user.salary
      this.editForm._id = this.user._id
    },
    updateUser: function () {
        this.$emit("user-update", {id: this.editForm._id, salary: this.editForm.salary})
    },
    change: function (event) {
      this.editForm.salary = event.target.value
    }
  },
};
</script>

<style scoped>
button {
  margin-right: 10px;
}
</style>
