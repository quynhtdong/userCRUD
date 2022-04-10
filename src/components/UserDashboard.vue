<script>
import UserManagement from "./UserManagement.vue";
import UserTable from "./UserTable.vue";

export default {
  data: function () {
    return {
      data: [
        {
          _id: "5e5d8a33962020b0583a5ade",
          index: 1,
          isActive: false,
          salary: "$1,878.32",
          picture: "http://placehold.it/32x32",
          age: 34,
          eyeColor: "brown",
          name: "Jewel Sosa",
          gender: "female",
          company: "SIGNIDYNE",
          email: "jewelsosa@signidyne.com",
          phone: "+1 (817) 538-2348",
          address: "291 Kingston Avenue, Bannock, Washington, 8709",
        },
        {
          _id: "5e5d8a33d5668ba005759ac4",
          index: 2,
          isActive: false,
          salary: "$3,559.88",
          picture: "http://placehold.it/32x32",
          age: 23,
          eyeColor: "brown",
          name: "Grimes Olsen",
          gender: "male",
          company: "YURTURE",
          email: "grimesolsen@yurture.com",
          phone: "+1 (926) 502-3084",
          address: "377 Danforth Street, Cleary, Virginia, 6123",
        },
        {
          _id: "5e5d8a333296d622e5170499",
          index: 3,
          isActive: true,
          salary: "$2,300.27",
          picture: "http://placehold.it/32x32",
          age: 33,
          eyeColor: "brown",
          name: "Velasquez Bennett",
          gender: "male",
          company: "FUTURITY",
          email: "velasquezbennett@futurity.com",
          phone: "+1 (820) 452-3033",
          address: "605 Metrotech Courtr, Retsof, Kentucky, 2629",
        },
        {
          _id: "5e5d8a33668e01faecf43a21",
          index: 4,
          isActive: false,
          salary: "$2,123.47",
          picture: "http://placehold.it/32x32",
          age: 38,
          eyeColor: "green",
          name: "Gayle Burt",
          gender: "female",
          company: "VURBO",
          email: "gayleburt@vurbo.com",
          phone: "+1 (847) 419-3818",
          address: "319 Highland Avenue, Elizaville, Arkansas, 273",
        },
        {
          _id: "5e5d8a33e0911b7fc2d6e9f3",
          index: 5,
          isActive: true,
          salary: "$2,358.41",
          picture: "http://placehold.it/32x32",
          age: 32,
          eyeColor: "blue",
          name: "Lori Price",
          gender: "female",
          company: "GRUPOLI",
          email: "loriprice@grupoli.com",
          phone: "+1 (915) 511-3754",
          address: "904 Canal Avenue, Canoochee, Pennsylvania, 8762",
        },
        {
          _id: "5e5d8a3314b603b9ef876879",
          index: 6,
          isActive: false,
          salary: "$3,752.40",
          picture: "http://placehold.it/32x32",
          age: 31,
          eyeColor: "green",
          name: "Marissa Hines",
          gender: "female",
          company: "SNORUS",
          email: "marissahines@snorus.com",
          phone: "+1 (870) 512-3865",
          address: "326 Montieth Street, Stouchsburg, Guam, 5638",
        },
        {
          _id: "5e5d8a3349fecb478c4037bc",
          index: 7,
          isActive: false,
          salary: "$1,792.48",
          picture: "http://placehold.it/32x32",
          age: 20,
          eyeColor: "brown",
          name: "Polly Payne",
          gender: "female",
          company: "STOCKPOST",
          email: "pollypayne@stockpost.com",
          phone: "+1 (997) 501-2848",
          address: "286 Canda Avenue, Yardville, Indiana, 5281",
        },
      ],
      show: [],
      editForm: {
        _id: "",
        name: "",
        salary: "",
      },
      newUser: {
        _id: "",
        index: 0,
        isActive: false,
        salary: "",
        company: "",
      },
    };
  },

  components: {
    UserManagement,
    UserTable,
  },
  methods: {
    delUser: function (id) {
      let index = this.data.findIndex((user) => {
        return user._id === id;
      });
      this.data.splice(index, 1);
    },

    showUsers: function () {
      this.show = this.data;
    },

    updateUser: function (val) {
      this.data.some((user) => {
        if (user._id == val.id) {
          user.salary = val.salary;
          return true;
        }
      });
    },

    addUser: function (user) {
      this.data.push(user);
      document.getElementById("username-add").value = "";
      document.getElementById("company-add").value = "";
      document.getElementById("salary-add").value = "";
      this.newUser = {
        _id: "",
        index: 0,
        isActive: false,
        salary: "",
        company: "",
      };
    },
  },
};
</script>

<template>
  <UserManagement
    :data="data"
    :newUser="newUser"
    @show-users="showUsers()"
    @add-user="addUser($event)"
  />
  <UserTable
    :show="show"
    :editForm="editForm"
    @user-del="delUser($event)"
    @user-update="updateUser($event)"
  />
</template>
<style></style>
