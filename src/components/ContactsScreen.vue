<template>
  <div :class="{ home: !show }">
    <h1>{{ title }}</h1>
    <div class="contactsBtn">
      <button @click="showContact">
        <span v-if="show">Hide contacts</span>
        <span v-else>Show contacts</span>
      </button>
    </div>
    <div v-if="show">
      <div class="favBtn">
        <button @click="showFavourite">
          <span v-if="showFav">Hide favourite</span>
          <span v-else>Show favourites</span>
        </button><br>
        <input v-model="query" id="searchBar" type="text" placeholder="Search name">
      </div>
      <div v-if="showFav">
        <Table :user="user" :collection="filterFavUsers" />
      </div>
      <div v-else-if="query">
        <Table :user="user" :collection="searchUser" />
      </div>
      <div v-else>
        <Table :user="user" :collection="users" />
      </div>
    </div>
  </div>
</template>

<script>
import Table from "./Table.vue";
export default {
  data() {
    return {
      title: "Contacs",
      show: false,
      users: [],
      user: null,
      showFav: false,
      query: null 
    };
  },
  components: {
    Table,
  },
  methods: {
    showContact() {
      this.show = !this.show;
    },
    showFavourite() {
      this.showFav = !this.showFav;
    }
  },
  computed: {
    users() {
      this.users.forEach((u) => {
        u = Object.assign({}, u, { isFavourite: false });
      });
      return this.users;
    },
    filterFavUsers() {
      return this.users.filter((u) => u.isFavourite);
    },
    searchUser(){
        if(this.query){
          return this.users.filter((u) => u.name.toLowerCase().includes(this.query.toLowerCase()))
        }
    }
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/users")
      .then((res) => res.json())
      .then((data) => (this.users = data))
      .catch((err) => console.log(err.message));
  },
};
</script>

<style scoped>
.favBtn,
.contactsBtn {
  text-align: center;
  margin-top: 20px;
}
.contactsBtn button,
.favBtn button {
  width: 200px;
  height: 44px;
  border-radius: 4px;
  padding: 8px;
  font-size: 1rem;
}
.favBtn button {
  border: solid #c94c4c;
  background-color: white;
  color:#212427;
}
.contactsBtn button {
  border: solid #c94c4c;
  background-color: #c94c4c;
  color: white;
}
h1 {
  text-align: center;
  margin-top: 10px;
  font-size: 40px;
  color:#212427;
}
.home {
  background-image: url("/src/assets/meeting-g4621478be_1280.png");
  background-repeat: no-repeat;
  background-size: 400px;
  background-position: 50%;
  height: 100vh;
  margin-top: 50px;
}
.home h1 {
  font-size: 100px;
}
#searchBar{
  margin-top: 20px;
  width: 50%;
  height:20px;
  font-size: 1rem;
  padding: 10px;
  background-color:rgb(248, 255, 248);
  border-color: #212427;
}
@media (max-width: 542px){
  #searchBar{
    width: 90%;
  }
  .home {
    background-image: none;
    margin: 200px auto;
    text-align: center !important;
  }
  .home h1 {
    font-size: 50px;
  }
}
</style>
