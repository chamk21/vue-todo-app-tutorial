<template>
    <div>
        <form v-on:submit="addTodo">
            <input v-model='title' type="text" name='title' placeholder="add a todo">
            <input type="submit" value='submit' class="btn">
        </form>    
    </div>
</template>

<script>

//import { v4 as uuidv4 } from 'uuid';
export default {
    name:'AddTodo',
    data(){
        return {
            title: ''
        }
    },
    methods:{
        addTodo(e){
            e.preventDefault();
            const newTodo = {
                title: this.title,
                complete: false
            }

            this.$emit('add-todo', newTodo);
            this.title= ''
 
        }
    }

}
</script>
<style scoped>
form {
    display: flex;
  }
  input[type="text"] {
    flex: 10;
    padding: 5px;
  }
  input[type="submit"] {
    flex: 2;
  }
</style>