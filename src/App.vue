<template>
  <div id="app">
    <Header />
  </div>
</template>

<script>
import Header from './components/Header.vue';

export default {
  components: {
    Header,
  },
};

// $color-primary: #55c57a;
// $color-primary-light: #7ed56f;
// $color-primary-dark: #28b485;

// $color-secondary-light: #ffb900;
// $color-secondary-dark: #ff7730;

// $color-tertiary-light: #2998ff;
// $color-tertiary-dark: #5643fa;

// $color-grey-light-1: #f7f7f7;
// $color-grey-light-2: #eee;
// $color-grey-dark: #777;
// $color-white: #fff;
// $color-black: #000;
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;500;600;700;800&display=swap');

*,
*::before,
*::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  font-size: 62.5%;
}

body {
  font-family: 'Montserrat', sans-serif;
  font-size: 1.6rem;
  color: #333;
  background-color: #f7f7f7;
}

.container {
  max-width: 114rem;
  margin: 1.5rem auto 2rem auto;
  height: auto;
  padding: 2rem 2rem;
}

.btn {
  display: inline-block;
  padding: 1rem 2.5rem;
  text-transform: uppercase;
  border-radius: 10rem;
  box-shadow: 0 0.5rem 1.5rem rgba(0, 0, 0, 0.3);
  outline: none;
  border: none;
  cursor: pointer;
  transition: transform 0.3s;
}

.btn--white {
  background: #fff;
  color: #000;
}

.btn--green {
  background-color: #55c57a;
  color: #000;
}

.btn:hover {
  transform: scale(1.1) translateY(-3px);
  box-shadow: 0 1rem 2rem rgba(0, 0, 0, 0.3);
}

.btn:active {
  transform: scale(1.1) translateY(-1px);
  box-shadow: 0 0.5rem 1.5rem rgba(0, 0, 0, 0.3);
}
.no-user {
  font-size: 3rem;
  text-transform: uppercase;
  color: black;
  text-align: center;
  margin: 2.5rem auto;
}
</style>
