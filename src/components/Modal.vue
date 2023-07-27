<template>
  <div class="modalBacground">
    <div class="modal">
      <p class="closeBtn" @click.self="close">&times;</p>
      <h2 class="header">{{ user.name }}</h2>
      <table>
        <tr>
          <td class="rowTitle">Adress</td>
          <td>
            {{ user.address.suite }} {{ user.address.street }}<br />
            {{ user.address.city }} {{ user.address.zipcode }}
          </td>
        </tr>
        <tr>
          <td class="rowTitle">Phone</td>
          <td>{{ user.phone }}</td>
        </tr>
        <tr>
          <td class="rowTitle">Website</td>
          <td>
            <a href="user.website">{{ user.website }}</a>
          </td>
        </tr>
        <tr>
          <td class="rowTitle">Company</td>
          <td>{{ user.company.name }}</td>
        </tr>
        <tr>
          <td class="rowTitle">Catchphrase</td>
          <td>
            <i>"{{ user.company.catchPhrase }}"</i>
          </td>
        </tr>
        <tr>
          <td class="rowTitle">BS</td>
          <td>{{ user.company.bs }}</td>
        </tr>
        <tr>
          <td class="rowTitle">Coordinates</td>
          <td>
            {{ user.address.geo.lat }}<br />
            {{ user.address.geo.lng }}
          </td>
        </tr>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  props: ["address", "user"],
  methods: {
    close() {
      this.$emit("close");
    },
  },
};
</script>
<style scoped>
.modal {
  width: 60%;
  height: auto;
  padding: 20px;
  background: white;
  border-radius: 10px;
  margin: 10% auto;
  color: #212427;
}
.modalBacground {
  top: 0;
  background-color: rgba(0, 0, 0, 0.5);
  width: 100%;
  height: 100%;
  position: fixed;
}
.header {
  text-align: center;
  margin-bottom: 20px;
  font-weight: bold;
}
table td {
  padding: 5px;
}
table tr {
  height: 20px;
}
table {
  margin: auto;
  text-align: left;
  width: 90%;
}
.rowTitle {
  font-weight: bold;
  width: 40%;
  background-color: #b1cbbb;
}
table tr:nth-child(odd) {
  background-color: #deeaee;
}
.closeBtn {
  font-size: 30px;
  float: right;
  transform: translateY(-10px);
}
.closeBtn:hover {
  cursor: default;
}
@media (max-width: 1090px) {
  .modal {
    width: 100%;
    height: 100%;
    margin-top: 0px;
    overflow-y: scroll;
    padding: 0px;
    border-radius: 0px;
  }
  table {
    width: 100%;
    margin:0px;
  }
  table td,
  .rowTitle {
    width: 100%;
    display: block;
    padding: 10px;
  }
  table td {
    background-color: white;
  }
  .closeBtn {
  font-size: 30px;
  transform: translate(-30px, 13px);
}
.header{
  margin-top: 20px;
}
}
</style>