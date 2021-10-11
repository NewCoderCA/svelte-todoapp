<script>
    import { createEventDispatcher } from 'svelete';
    import { fly } from 'svelte/transition';
 
 //Pulling Todoitem properties from object as single elements passing as parameters in components 
    export let id;
    export let title;
    export let completed;
 
    const dispatch = createEventDispatcher();
 
 //User hits x dispatch new event and delete id using eventhandler switches to handleDeleteTodo and removes item
 function deleteTodo() {
    dispatch('deleteTodo', {
        id: id
    });
 }
 
 //Function handles by passing id property in event.detail object checks which state should be toggled
 function toggleComplete() {
     dispatch('toggleComplete', {
         id: id
     });
 }
 </script>
 
 
 
 <div class="todo-item"> 
     <!--Animation transition appearance of todo item using in-built-svelte fly -->
     <div class="todo-item-left" transition:fly={{ y: 20, duration: 300}}>
         <input type="checkbox" bind:checked={completed} on:change={toggleComplete}>
         <div class="todo-item-label" class:completed={completed}>{title}</div>
     </div>
     <div class="remove-item" on:click={deleteTodo}>x</div>
 </div>
 
 
 
 <style>
   .todo-item {
       margin-bottom: 15px;
       display: flex;
       align-items: center;
       justify-content: space-between;
       animation-duration: 0.2s;
   }
   .todo-item-left {
       display: flex;
       align-items: center;
   }
   .todo-item-label {
       border: 1px solid white;
       margin-left: 12px;
   }
   .remove-item {
       cursor: pointer;
       margin-left: 15px;
   }
   .remove-item:hover {
       color:cyan;
   }
   .completed {
       text-decoration: line-through;
       color: grey;
 }
 </style>