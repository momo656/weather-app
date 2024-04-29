<template>
<div>
  <main>
    <div class="search-box">
    <input type="text" v-model="city" class="search-bar" placeholder="Enter Your City">

</div>
  </main>
</div>
</template>

<script>

export default {
    name: 'HelloWorld',
    props: {
        msg: String
    },
    data() {
        return {
            city: ''
        }

    },
    
    
}
</script>

<style scoped>
.search-box .search-bar{
    width: 80%;
    padding: 10px;
    border-radius:  15px 0px 15px 0px ;
    border: 1px solid #ccc;
    font-size: 16px;
    margin: 20px auto;
    
   
} 
main{
  height: 100vh;
  padding: 5px;
  background-image: linear-gradient(rgba(0,0,0,0.7), rgba(0,0,0,0.7)), url('./assets/img-1.jpg');
}

</style>
