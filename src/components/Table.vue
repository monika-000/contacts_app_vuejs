 <template>
  <div>
    <table class="contactsTable">
      <thead>
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th>Username</th>
          <th>Email</th>
          <th>Details</th>
          <th>Add to favourite</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in collection" :key="user.id">
          <td data-title="Id">{{ user.id }}</td>
          <td data-title="Name">{{ user.name }}</td>
          <td data-title="Username">{{ user.username }}</td>
          <td data-title="Email">{{ user.email }}</td>
          <td data-title="Details" class="details">
            <button @click="showDetails(user)" class="detailsBtn">
              View details
            </button>
          </td>
          <td data-title="Add to favourite" class="icon">
            <a @click="addToFav(user)" :class="{ fav: user.isFavourite }"
              ><i class="fa fa-heart"></i
            ></a>
          </td>
        </tr>
      </tbody>
    </table>
    <div v-if="modalShow">
      <Modal :user="userToShow" @close="showDetails(user)" />
    </div>
  </div>
</template>

<script>
import Modal from "./Modal.vue";
export default {
  data() {
    return {
      modalShow: false,
      showFav: false,
      userToShow: null,
    };
  },
  components: {
    Modal,
  },
  props: ["collection", "user"],
  methods: {
    addToFav(u) {
      u.isFavourite = !u.isFavourite;
    },
    showDetails(u) {
      this.userToShow = u;
      this.modalShow = !this.modalShow;
    },
  },
};
</script>
 <style scoped>
.contactsTable {
  width: 90%;
  margin: 30px auto;
  table-layout: fixed;
  color:#212427;
}
thead th {
  font-weight: bold;
  text-align: start;
  background-color: #b1cbbb;
  top: 0;
  position: sticky;
}
table tr {
  text-align: start;
}
table th,
table td {
  padding: 10px;
  font-size: 1rem;
}
.details,
.icon {
  text-align: center !important;
}
.fav {
  color: #c94c4c;
}
.fa-heart {
  font-size: 30px;
}
tbody tr:nth-child(odd) td {
  background-color: #deeaee;
}
.detailsBtn {
  background-color: #eea29a;
  border: #eea29a;
  height: 30px;
  border-radius: 4px;
  padding: 8px;
  font-size: 1rem;
}
@media (max-width: 1172px) {
  .contactsTable {
    border: 2px solid #b1cbbb;
  }
  table thead tr {
    display: none;
  }
  table tr {
    display: block;
  }

  table td {
    padding: 10px;
  }
  table td,
  .details,
  .icon {
    text-align: right !important;
    display: block;
  }
  table td::before {
    content: attr(data-title) ": ";
    float: left;
  }
  .detailsBtn{
    color: #212427;
  }
}
</style>
 