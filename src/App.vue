<template>
  <div id="app">
    <form id="main">
      <h1> Services </h1>

      <nav>
        <a href="#"
          v-for="(service, index) in services" :key='index'
          :class="[optedServices.indexOf(service.name) >= 0 ? 'selected' : 'unselected']"
          @click="chooseService(index)"
        >
        {{ service.name }} <span> {{ service.price | currency }} </span>
        <br>
        </a>
      </nav>

      <div class="total">
        Total: <span> {{ total | currency }}</span>
      </div>
      </form>
  </div>

</template>

<script>

export default {
  name: 'app',
  components: {
  },
  data(){
    return{
      services:[
        {name: 'Web Development', price: 300},
        {name: 'Design', price: 400},
        {name: 'Integration', price: 250},
        {name: 'Deployment', price: 150},
        {name: 'Training', price: 220}
      ],
      total: 0,
      optedServices: []
    }
  },
  methods:{
    chooseService(index){
      if(this.optedServices.indexOf(this.services[index].name) < 0){
        this.total = this.total + this.services[index].price;
        this.optedServices.push(this.services[index].name);
      }
      else{
        this.total = this.total - this.services[index].price;
        //this.optedServices.pop(this.services[index].name);
        //this.optedServices = this.optedServices.filter(serv => serv.name === this.services[index].name);
        this.optedServices = this.optedServices.filter(serv => serv != this.services[index].name);
      }
    }
  },
  created(){
      this.total = this.services[0].price;
      this.optedServices.push(this.services[0].name);
  },
  filters:{
    currency(val){
      return "$" + val.toFixed(2);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
form h1{
    color:#fff;
    font-size:64px;
    font-family:'Cookie', cursive;
    font-weight: normal;
    line-height:1;
    text-shadow:0 3px 0 rgba(0,0,0,0.1);
}
nav{
    display:block;
    /*margin:60px auto 45px;*/
    background-color:#5597b4;
    box-shadow:0 1px 1px #ccc;
    border-radius:2px;
}
nav a{
    display:block;
    padding: 18px 30px;
    /*color:#fff !important;*/
    font-weight:bold;
    font-size:16px;
    text-decoration:none !important;
    line-height:1;
    /*text-transform: uppercase;*/
    background-color:transparent;
}
nav a span{
  float:right;
}

.unselected{
  background: lightblue;
  border:none;
}
.selected{
  background:lightpink;
  border:none;
}
form{
    background-color: #61a1bc;
    border-radius: 2px;
    box-shadow: 0 1px 1px #ccc;
    width: 400px;
    padding: 35px 60px;
    margin: 50px auto;
}

form h1{
    color:#fff;
    font-size:64px;
    font-family:'Cookie', cursive;
    font-weight: normal;
    line-height:1;
    text-shadow:0 3px 0 rgba(0,0,0,0.1);
}

form ul{
    list-style:none;
    color:#fff;
    font-size:20px;
    font-weight:bold;
    text-align: left;
    margin:20px 0 15px;
}

form nav a{
    padding:20px 30px;
    background-color:#e35885;
    margin-bottom:8px;
    box-shadow:0 1px 1px rgba(0,0,0,0.1);
    cursor:pointer;
}

form nav a span{
    float:right;
}

form nav a.selected{
    background-color:#8ec16d;
}

div.total{
    border-top:1px solid rgba(255,255,255,0.5);
    padding:15px 30px;
    font-size:20px;
    font-weight:bold;
    text-align: left;
    color:#fff;
}

div.total span{
    float:right;
}
</style>
