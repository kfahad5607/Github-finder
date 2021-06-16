<template>
  <div class="container">
    <div v-if="user">
      <section class="main">
        <div class="main__avatar-box">
          <img
            :src="user.avatar_url"
            :alt="`Avatar of ${user.name}`"
            class="main__avatar"
          />
          <p class="main__name">{{ user.name ? user.name : 'Github User' }}</p>
          <p class="main__username">{{ user.login }}</p>
          <p class="main__location">
            <i class="fa fa-map-marker" aria-hidden="true"></i>
            <span class="main__location-text">{{
              user.location ? user.location : 'Earth'
            }}</span>
          </p>
        </div>
        <div class="main__content">
          <span class="bio-label">Bio</span>
          <p class="bio">
            {{ user.bio ? user.bio : 'No bio available' }}
          </p>

          <div class="info-container">
            <div class="info-box">
              <p class="text">
                {{ user.company ? user.company : 'Unavailable' }}
              </p>
              <span class="label">Company</span>
            </div>

            <div class="info-box">
              <p class="text" v-if="user.blog">
                <a :href="user.blog">{{ user.blog }}</a>
              </p>
              <p class="text" v-else>Unavailable</p>
              <span class="label">Website</span>
            </div>

            <div class="info-box">
              <p class="text" v-if="user.email">
                <a :href="`mailto:${user.email}`">{{ user.email }}</a>
              </p>
              <p class="text" v-else>Unavailable</p>
              <span class="label">Email</span>
            </div>
          </div>

          <div class="info-container">
            <div class="info-box">
              <p class="number">{{ user.followers }}</p>
              <span class="label">Followers</span>
            </div>

            <div class="info-box">
              <p class="number">{{ user.following }}</p>
              <span class="label">Following</span>
            </div>

            <div class="info-box">
              <p class="number">{{ user.public_repos }}</p>
              <span class="label">Public Repos</span>
            </div>

            <div class="info-box">
              <p class="number">{{ user.public_gists }}</p>
              <span class="label">Public Gists</span>
            </div>
          </div>

          <div class="link-box">
            <a href="#" class="visit__link">Visit Profile</a>
          </div>
        </div>
      </section>
      <section class="repos-box">
        <h2>Public Repositories</h2>

        <p v-if="repos.length === 0">No Repositories</p>
        <div v-else>
          <article class="repo" v-for="(repo, index) in repos" :key="index">
            <a :href="repo.html_url" class="repo-name">{{ repo.name }}</a>
          </article>
        </div>
      </section>
    </div>
    <p class="no-user" v-else>Loading...</p>
  </div>
</template>

<script>
export default {
  props: ['username'],
  data() {
    return {
      user: null,
      repos: [],
    };
  },
  mounted() {
    fetch('https://api.github.com/users/' + this.username)
      .then((res) => res.json())
      .then((data) => (this.user = data))
      .catch((err) => console.log('ERROR ==>', err.message));

    fetch('https://api.github.com/users/' + this.username + '/repos')
      .then((res) => res.json())
      .then((data) => (this.repos = data))
      .catch((err) => console.log('ERROR ==>', err.message));
  },
};
</script>

<style>
.main {
  margin-bottom: 2rem;
  border-radius: 3rem;
  background: rgb(126, 213, 111);
  box-shadow: 0 0.5rem 2rem rgba(0, 0, 0, 0.2);
  overflow: hidden;
}

.main::after {
  content: '';
  display: block;
  clear: both;
}

.main__avatar-box {
  width: 25%;
  padding: 3rem 2rem;
  height: 100%;
  text-align: center;
  float: left;
}

.main__avatar {
  display: block;
  width: 15rem;
  border-radius: 50%;
  margin: 0 auto;
}

.main__name {
  padding: 0.5rem;
  margin-top: 0.5rem;
  font-size: 1.8rem;
  font-weight: 700;
  color: black;
}

.main__username {
  padding: 0 0.5rem 0 0.5rem;
  margin-bottom: 1rem;
  font-size: 1.6rem;
  font-weight: 500;
  color: #222;
}

.main__username::before {
  content: '@';
}

.main__location {
  font-size: 1.8rem;
  color: #222;
}

.main__location-text {
  margin-left: 0.8rem;
}

.main__content {
  width: 75%;
  height: auto;
  padding: 2rem;
  float: right;
}

.bio-label {
  display: block;
  font-size: 2rem;
  font-weight: 700;
  color: black;
  text-align: center;
  margin-bottom: 0.5rem;
}

.bio {
  text-align: center;
  font-size: 1.8rem;
  font-weight: 500;
  color: #222;
}

.label {
  font-size: 2rem;
  font-weight: 400;
  color: black;
}

.info-container {
  text-align: center;
  margin: 2rem 0;
}

.info-box {
  display: inline-block;
  padding: 1rem 1.5rem;
  text-align: center;
}

.text {
  font-size: 1.6rem;
  font-weight: 500;
  color: black;
  margin-bottom: 0.5rem;
}

.text a {
  text-decoration: none;
  color: inherit;
}

.number {
  font-size: 4rem;
}

.link-box {
  text-align: center;
  margin-bottom: 2rem;
}

.visit__link {
  display: inline-block;
  text-decoration: none;
  font-size: 2rem;
  background-color: rgb(255, 255, 255);
  color: rgb(0, 0, 0);
  color: rgb(255, 255, 255);
  background-color: rgb(0, 0, 0);
  padding: 0.9rem 1.5rem;
  border-radius: 3px;
  text-align: center;
  width: auto;
}

.repos-box {
  height: auto;
  text-align: center;
  overflow: hidden;
}

.repos-box h2 {
  font-size: 2.5rem;
  text-transform: uppercase;
  text-align: center;
  margin: 1rem 0;
}

.repo {
  display: inline-block;
  box-shadow: 0 0.5rem 2rem rgba(0, 0, 0, 0.2);
  height: auto;
  width: 48%;
  border-radius: 1rem;
  padding: 1rem;
  margin: 1rem 0.8rem;
  background: rgb(126, 213, 111);
  overflow: hidden;
}

.repo-name {
  font-size: 1.9rem;
  font-weight: 700;
  text-decoration: none;
  color: black;
}

/* MEDIA QUERIES */

@media screen and (max-width: 840px) {
  .number {
    font-size: 3.5rem;
    font-weight: 500;
  }
  .main__avatar-box {
    width: 100%;
  }

  .main__content {
    width: 100%;
  }

  .repo {
    width: 95%;
  }
}
</style>
