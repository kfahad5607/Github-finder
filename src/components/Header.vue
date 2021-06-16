<template>
  <div>
    <header class="header">
      <div class="brand">
        <router-link to="/">
          <div class="brand__icon">
            <i class="fab fa-github"></i>
          </div>
          <div class="brand__name">Github Finder</div>
        </router-link>
      </div>
      <nav class="navigation">
        <ul class="navigation__links">
          <li>
            <router-link
              to="/"
              class="navigation__link navigation__link--active"
              >Home</router-link
            >
          </li>
          <li>
            <router-link to="/about" class="navigation__link"
              >About</router-link
            >
          </li>
        </ul>
      </nav>
    </header>
    <router-view />
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.header {
  background-image: linear-gradient(
    to right,
    rgb(39, 180, 133, 0.8),
    rgba(126, 213, 111, 0.8)
  );
  width: 100%;
}

.header::after {
  content: '';
  display: block;
  clear: both;
}

.brand {
  float: left;
  padding: 2rem 3rem;
  font-size: 3rem;
  color: #000;
}

.brand a,
.brand a:visited,
.brand a:active {
  text-decoration: none;
  color: black;
}

.brand__icon {
  display: inline-block;
  margin-right: 1rem;
}

.brand__name {
  display: inline-block;
  font-weight: 700;
}

.navigation {
  float: right;
  padding: 2rem 3rem;
}

.navigation__links {
  list-style: none;
}

.navigation__links li {
  display: inline-block;
  margin: 0 1.5rem;
}

.navigation__link,
.navigation__link:visited {
  background: transparent;
  border: none;
  color: #000;
  cursor: pointer;
  display: inline-block;
  font-weight: 500;
  outline: none;
  padding: 1rem 1rem;
  position: relative;
  text-decoration: none;
  text-transform: uppercase;
  text-transform: uppercase;
  transition: color 0.3s;
  z-index: 1;
}

.navigation__link::after {
  content: '';
  display: block;
  background-color: #000;
  border-radius: 0.3rem;
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  height: 5%;
  z-index: -1;
  transition: height 0.3s;
}

.navigation__link:hover,
.navigation__link.router-link-exact-active {
  color: #fff;
}

.navigation__link:hover::after,
.router-link-exact-active::after {
  height: 100%;
}

/* MEDIA QUERIES */
@media screen and (max-width: 590px) {
  .brand {
    width: 100%;
    color: red;
    text-align: center;
    padding-top: 1.5rem;
    padding-bottom: 0.5rem;
  }

  .navigation {
    width: 100%;
    text-align: center;
    padding-top: 0.5rem;
    padding-bottom: 1.5rem;
  }
}

/* @media screen and (max-width: 420px) {
  .brand {
    width: 100%;
    color: red;
    text-align: center;
    padding-top: 1.5rem;
    padding-bottom: 0.5rem;
  }

  .navigation {
    width: 100%;
    text-align: center;
    padding-top: 0.5rem;
    padding-bottom: 1.5rem;
  }
} */
</style>
