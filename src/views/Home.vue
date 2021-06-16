<template>
  <div class="container">
    <div class="search-box">
      <input
        type="search"
        name="search"
        v-model="query"
        autocomplete="off"
        placeholder="Search users..."
        class="search-box__input"
      />
      <button class="search-box__btn btn--green" @click="getUsers">
        search
      </button>
    </div>
    <button class="clear-btn" @click="clearUsers" v-show="users.length > 0">
      Clear
    </button>
    <p class="no-user" v-if="userCount === 0">No user found!</p>
    <section class="cards-box" v-else>
      <article class="card" v-for="(user, index) in users" :key="index">
        <div class="card__avatar">
          <img :src="user.avatar_url" alt="" />
        </div>
        <div class="card__content">
          <p class="card__name"><a :href="user.html_url">Visit Github</a></p>
          <p class="card__username">
            <span>{{ user.login }}</span>
          </p>
          <router-link
            :to="{ name: 'Detail', params: { username: user.login } }"
            class="card__link"
            >More</router-link
          >
        </div>
      </article>
    </section>
  </div>
</template>

<script>
export default {
  name: 'Home',
  components: {},
  data() {
    return {
      query: '',
      userCount: null,
      users: [],
    };
  },
  methods: {
    getUsers() {
      if (this.query) {
        fetch('https://api.github.com/search/users?q=' + this.query)
          .then((res) => res.json())
          .then((data) => {
            this.users = data.items;
            this.userCount = data.total_count;
          })
          .catch((err) => console.log('ERROR ==>', err.message));

        this.query = '';
      }
    },
    clearUsers() {
      this.users = [];
    },
  },
};
</script>

<style scoped>
/* Search box */

.search-box {
  border-radius: 10rem;
  background-color: #fff;
  overflow: hidden;
  position: relative;
  box-shadow: 0.5rem 0.7rem 3rem rgba(0, 0, 0, 0.1);
}

.search-box__input {
  border: none;
  padding: 2rem 3rem;
  width: calc(100% - 11rem);
  outline: none;
  font-size: 1.8rem;
}

.search-box__btn {
  display: inline-block;
  padding: 1.5rem 2.5rem;
  text-transform: uppercase;
  border-radius: 10rem;
  outline: none;
  border: none;
  cursor: pointer;
  position: absolute;
  right: 0.7rem;
  top: 50%;
  transform: translateY(-50%);
  transition: transform 0.3s;
}

.search-box__btn:active {
  transform: translateY(-50%) scale(0.95);
}

.clear-btn {
  display: block;
  text-transform: uppercase;
  font-size: 1.8rem;
  font-weight: 400;
  padding: 1rem 1.5rem;
  border: none;
  border-radius: 10rem;
  margin: 2rem auto;
  width: 97%;
  background-color: rgb(0, 0, 0);
  color: #fff;
  cursor: pointer;
  transition: all 0.3s;
}

.clear-btn:hover {
  background-color: #333;
}

.clear-btn:active {
  transform: scale(0.99);
}

/* Cards */
.cards-box {
  margin: 2rem auto 1rem auto;
  text-align: center;
}

.card {
  display: inline-block;
  border: 1px solid #28b485;
  width: 33rem;
  height: 15rem;
  padding: 1.5rem;
  margin: 1rem 1.5rem;
  background-image: linear-gradient(to right bottom, #28b485, #7ed56f);
  box-shadow: 0 0.5rem 2rem rgba(0, 0, 0, 0.2);
  border-radius: 0.4rem;
  position: relative;
}

.card::after {
  content: '';
  display: block;
  clear: both;
}

.card__avatar {
  position: absolute;
  top: 50%;
  left: 4%;
  transform: translate(0, -50%);
  width: 10rem;
  float: left;
}

.card__avatar img {
  width: 10rem;
  height: 10rem;
  border-radius: 50%;
}

.card__content {
  float: right;
  position: absolute;
  top: 50%;
  right: 4%;
  transform: translate(0, -50%);
  width: 18rem;
}

.card__name {
  display: block;
  padding: 0.5rem;
  font-size: 1.8rem;
  font-weight: 700;
  color: black;
}

.card__name a {
  text-decoration: none;
  color: inherit;
  text-transform: uppercase;
}

.card__username {
  padding: 0 0.5rem 0 0.5rem;
  margin-bottom: 1rem;
  font-size: 1.6rem;
  font-weight: 500;
  color: #222;
  width: 99%;
  word-break: break-all;
}

.card__username::before {
  content: '@';
}

.card__link {
  display: inline-block;
  text-decoration: none;
  text-transform: uppercase;
  background-color: rgb(255, 255, 255);
  color: rgb(0, 0, 0);
  color: rgb(255, 255, 255);
  background-color: rgb(0, 0, 0);
  padding: 0.7rem 1.3rem;
  border-radius: 3px;
}

/* MEDIA QUERIES */
@media screen and (max-width: 410px) {
  .no-user {
    font-size: 2.5rem;
  }
  .card {
    height: auto;
    width: 90%;
  }
  .card__avatar {
    width: 100%;
    position: static;
    transform: translate(0);
    margin-bottom: 1rem;
  }

  .card__content {
    width: 100%;
    position: static;
    transform: translate(0);
  }
}
</style>
