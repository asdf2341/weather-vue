<template>
<div className="user">
<button v-on:click="DeleteUser(index)" >Delete</button>
 <h3>{{ user.name }}</h3>
 <p>{{user.email}}-<b>{{ user.pass }}</b></p>

</div>
</template>

<script>
export default{
    props:{
        user:{
            type:Object,
            required:true
        },
        index:{
            type:Number,
            required:true
        },
        DeleteUser:{
            type:Function,
            required:true
        },
    }
    
}
</script>

<style scoped>
button{
  border-radius: 5px;
  border:1px solid silver;
  background-color:rgb(197, 58, 58);
  padding:20px 30px;
  cursor:pointer;
  transition:transform 500ms ease;
  font-weight: bold;
  color:white;
  float:right;

}
button:hover{
  transform:translateY(-5px)
}
</style>