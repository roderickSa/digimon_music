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
    --orange: #FF542B;
    --yellow: rgb(255, 235, 59);
    --violet: #ee82ee;
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
html::-webkit-scrollbar-thumb{
    background: #2196f3;
    border-radius: 5rem;
}
/* html::-webkit-scrollbar-thumb{
    background: #2196f3;
    border-radius: 5rem;
}*/
/*.box-container::-webkit-scrollbar {
  background: #2196f3;
  color: #fff;
  width: .8rem;
  border-radius: 5rem;
}*/
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
    background: var(--yellow);
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
  /* flex: 1 1 15rem; */
  height: 12rem;
  position: relative;
  box-shadow: 0 0.5rem 1rem rgb(0 0 0 / 30%);
  border-radius: 50%;
  overflow: hidden;
  cursor: pointer;
}
.box.selected_digimon{
  border: 0.7rem solid #ffeb3b;
}
.box img{
  height: 100%;
  border-radius: 50%;
  object-fit: cover;
}
/* .music-navigation{
  height: 5rem;
  display: flex;
  justify-content: center;
  align-items: center;
} */
.music-container,
.music-navigation,
.music-image{
  width: 33.33%;
  height: 5rem;
  display: flex;
  justify-content: center;
  align-items: center;
}
.music-description{
  height: 5rem;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  overflow: hidden;
}
.music-description p{
  color: #fff;
  font-size: 1.7rem;
  width: 80%;
  overflow: hidden;
  text-align: center;
  animation: slider 4s linear infinite;
  padding-right: 200%;
  /*ayuda a para simular que hay 2 elementos uno detras de otro(al apareceer por el lado inicial aparece de golpe, bueno...)*/
}
@keyframes slider{
  0% {
        transform: translate(0, 0);
  }
  100% {
      transform: translate(100%, 0);
  }
}
.music-image .content-progress{
  background: #fff;
  height: 0.7rem;
  width: 80%;
  border-radius: 3.5rem;
  text-align: center;
  cursor: pointer;
}
.music-image .content-progress .progress{
  background: var(--yellow);
  height: 100%;
  border-radius: 3.5rem;
  width: 0;
}
.music-navigation button{
  border: 0.1rem solid rgba(0,0,0,0.7);
  height: 3.8rem;
  border-radius: 50%;
  margin: 0 1.3rem;
  width: 3.8rem;
  cursor: pointer;
  font-size: 1.5rem;
}
.digimon-crud{
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 1rem;
  align-items: center;
  background: var(--violet);
}
.digimon-crud .box-image-digimon-selected{
  flex: 1 1 45rem;
  display: flex;
  align-items: center;
  margin: 2rem 0;
}
.digimon-crud .box-image-digimon-selected img{
  margin: 0 auto;
  object-fit: cover;
}
.digimon-crud .form-digimon-selected{
  flex: 1 1 45rem;
  padding: 5rem 2rem;
  text-align: center;
}
.digimon-crud .form-digimon-selected h3{
  text-transform: uppercase;
  font-size: 2.5rem;
  color: #fff;
}
.inputBox{
  height: 5rem;
  background: var(--orange);
  border: 0.1rem solid rgba(0,0,0,0.3);
  margin-top: 1.5rem;
}
.inputBox select{
  width: 100%;
  height: 100%;
  background: none;
  padding-left: 1rem;
  font-size: 1.8rem;
}
@media only screen and (max-width: 576px) {
  .header{
    flex-direction: column;
  }
  .music-container, .music-navigation, .music-image{
    width: 100%;
  }
  .music-navigation button {
    height: 5rem;
    width: 5rem;
  }
  .music-image .content-progress{
    height: 1rem;
  }
}
</style>
