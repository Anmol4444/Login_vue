<template>
    <div>
        
      <main class="form-signin">
<div class="row">
<div class="propic col-md-4">
<img src="./assets/home.jpg" id="photo">
<input type="file" id="file">
<label for="file" id="uploadBtn">Choose photo</label>

</div>


<div class="left col-md-8">
  <form>
    <h1> Fill Up !</h1>
  
     <div class="mb-3">
   
    <input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Name*">
    <div id="emailHelp" class="form-text"></div>
  </div>
  <div class="mb-3">
    
    <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Email *">
    <div id="emailHelp" class="form-text"></div>
  </div>

   
     <div class="mb-3">
    
    <input type="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Number *">
    <div id="emailHelp" class="form-text"></div>
  </div>
  <select class="form-select" aria-label="Default select example">
  <option selected>Select Language</option>
  <option value="1">English</option>
  <option value="2">Nepali</option>
  
</select>


<select class="form-select" aria-label="Default select example" style='margin:15px 0px'>
  <option selected>Select Gender</option>
  <option value="1">Male</option>
  <option value="2">Female</option>
 
</select>
<div class="mb-3">
    <label for="exampleFormControlTextarea1" class="form-label"></label>
    <textarea class="form-control" id="exampleFormControlTextarea1" placeholder="Tell us about yourself" rows="3"></textarea>
  </div>

    

    <div class="checkbox mb-3">
      <label>
        <input type="checkbox" value="remember-me"> Remember me
      </label>
    </div>
    <button class="w-100 btn btn-lg btn-primary" type="submit" @onclick='addTodo'>Submit</button>
    
  </form>
  </div>
  </div>
</main>

       

        <ul  v-for="todo of todos" v-bind:key="todo.id">
            <li>{{todo.id}}}</li>
             <li>{{todo.name}}</li>
              <li>{{todo.email}}</li>
               <li>-{{todo.number}}</li>
                <li>{{todo.language}}</li>
             <!-- <li  v-for="todo of todos" v-bind:key="todo.id">{{todo.id}}--{{todo.email}}</li>
              <li  v-for="todo of todos" v-bind:key="todo.id">{{todo.number}}</li>
               <li  v-for="todo of todos" v-bind:key="todo.id">{{todo.Language}}</li>
             -->

        </ul>
    </div>
</template>

<script lang="ts">

import axios from 'axios';

const baseURL ="http://localhost:3000/todos";
export default{
    name: "Todo",

    data(){
        return{
            todos :[],
            todoName: '',
            todoEmail: '',
            todoNumber: '',
            todoLang: ''
        };
    },

    async created(){
        try{
           
             const res =await axios.get(baseURL);
             this.todos = res.data;

        }catch(e){
            console.error(e);
        }
    },
    methods:{
        async addTodo(){
            const res = await axios.post(baseURL,{name:this.todoName});

            this.todos = [...this.todos, res.data];

            this.todoName = '',
            this.todoEmail= '',
            this.todoNumber= '',
            this.todoLang= ''
        }
    }


}

</script>


<style>





.form-floating{
  margin: 20px 0px;
}

.form-signin {
 
  
  width: 100%;
  max-width: 830px;
  padding: 15px;
  margin: auto;
  border: 2px solid grey;
 
  box-shadow: 0 0 20px 10px rgba(37, 106, 172, 0.664); 
  top:40px;
}

.form-floating>.form-control
{
  height:30px;
}
.form-signin .checkbox {
  font-weight: 400;
}

.form-signin .form-floating:focus-within {
  z-index: 2;
}

.form-signin input[type="email"] {
  margin-bottom: -1px;
  border-bottom-right-radius: 0;
  border-bottom-left-radius: 0;
}

.form-signin input[type="password"] {
  margin-bottom: 10px;
  border-top-left-radius: 0;
  border-top-right-radius: 0;
}
.propic
{
  overflow: hidden;
  
}
.img{
  height: 200px;
  width: 200px;
}
#file
{
  display: none;
}
label{
    margin: 10px 0px;
    text-align: right;
}
#uploadBtn{
  position: absolute;
  text-align: center;
 left: 23.5%;
 top: 24%;
 cursor: pointer;
 background-color: grey;
  padding: 4px 50px;

}









li {
    list-style: none;
}

</style>