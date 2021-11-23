<template>
  <Home />
</template>

<script>
import Home from './components/Home.vue'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Nunito:wght@200;300;400;600;700&display=swap');

:root{
    --red: #ff3838;
    --orange: #FF542B;;
}
*{
    font-family: 'Roboto', sans-serif;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    outline: none;
    border: none;
    text-decoration: none;
    text-transform: capitalize;
    transition: .2s linear;
}
html{
    font-size: 62.5%;
    /* overflow-x: hidden; */
    scroll-padding-top: 9rem;
    scroll-behavior: smooth;
}
html::-webkit-scrollbar{
    width: .8rem;
}
html::-webkit-scrollbar-track{
    background: transparent;
}
/* html::-webkit-scrollbar-thumb{
    background: #2196f3;
    border-radius: 5rem;
} */
/* html::-webkit-scrollbar-thumb{
    background: #2196f3;
    border-radius: 5rem;
}
.box-container::-webkit-scrollbar {
  background: #2196f3;
  color: #fff;
  width: .8rem;
  border-radius: 5rem;
} */
*::selection{
    background-color: var(--red);
    color: #fff;
}
html{
    font-size: 62.5%;
    overflow-x: hidden;
    scroll-behavior: smooth;
    scroll-padding-top: 6rem;
}
body{
    background: #f7f7f7;
}
.box-container{
  display: flex;
  flex-direction: row;
  width: 100vw;
  overflow: auto;
  background: var(--orange);
}
.box-description{
  position: absolute;
  top: -100%;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, .9);
  text-align: center;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  word-break: break-word;
}
.box:hover .box-description,
.box:hover img{
  top: 0;
  transform: scale(1.2);
}
.box-description p{
  font-size: 1.4rem;
  padding: 1.3rem;
  font-weight: bold;
  display: flex;
  align-items: center;
}
.carrusel-digimon{
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  gap: 1.5rem;
}
.box{
  flex: 1 1 15rem;
  height: 15rem;
  position: relative;
  box-shadow: 0 0.5rem 1rem rgb(0 0 0 / 30%);
  border-radius: 50%;
  overflow: hidden;
  cursor: pointer;
}
.box img{
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
}
/* .box img:hover{
  transform: scale(1.2);
} */
</style>
