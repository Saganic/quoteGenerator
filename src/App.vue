<template>
  <div id="app">
    <Quote />
  </div>
</template>

<script>
import Quote from './components/Quote.vue';

export default {
  name: 'app',
  components: {
    Quote,
  },
};
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  padding:0 5%;
}
.section-header{
  display:flex;
  align-items: center;
}
.section-header h1{
  flex:1;

}
.section-header button{
  width:200px;
  height:40px;
  background-color:cadetblue;
  color:white;
  border:none;
  cursor: pointer;
  border-radius:5px;
}
section{
  border:1px solid rgb(201, 201, 201);
  border-radius:10px;
  padding:2%;
  display:flex;
}
section .col{
  flex:1;
}
section input{
  height:30px;
  padding:10px;
  min-width:200px;
  border:1px solid rgb(201, 201, 201);
  border-radius:5px;
}
section label{
  display:block;
  width:100%;
  margin-bottom:1rem;
}

table.col{
  text-align:left;
}
.search-box{
  width:300px;
  height:40px;
  padding:10px;
}
.total-container {
  flex:1;
  display:block;
  width:100%;
  text-align:right;
}
.modal{
    position:fixed;
    top:0;
    left:0;
    padding:3% 0;
    background-color:rgba(0,0,0,0.8);
    color:white;
    width:100%;
    height:100%;
    display:flex;
    justify-content: center;
  }
  .modal-inner{
    background-color:white;
    color:black;
    width:80vw;
    max-height:80vh;
    overflow-y:scroll;
    padding:2%;
  }
</style>
