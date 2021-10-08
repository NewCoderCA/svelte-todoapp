<script>
    import Todoitem from './Todos.svelte';

    //Variables
    let newToDoTitle = '';
    let currentFilter = 'all';
    let nextId = 4;

    let todos = [
        {
            id: 1,
            title: 'My first todo',
            completed: false
        },
        {
            id: 2,
            title: 'My second todo',
            completed: false
        },
        {
            id: 3,
            title: 'My third todo',
            completed: false
        }
    ];

// Adding New Todo
function addToDo(event) {
    if (event.key === 'Enter') {
 // Add new additional object to existing Todos items, increase id and reset title
        todos = [...todos, {
            id: nextId,
            completed: false,
            title: newToDoTitle
        }];
        nextId = nextId + 1;
        newToDoTitle = '';
    }
}

// Automatic reactive variables to filter to check number of uncompleted todos 
$: todosRemaining = filteredTodos.filter(todo => !todo.completed).length;
$: filteredTodos = currentFilter === 'all' ? todos : currentFilter === 'completed'
   ? todos.filter(todo => todo.completed)
   : todos.filter(todo => !todo.completed)

   
</script>

<div class="container">
    <img src={'./images/flagAfrica.png'} alt="Flags of African countries in African continent" class="logo">
    
    <h1>
        To Do App
    </h1>
    <input type="text" class="todo-input" placeholder="Insert to-do item" bind:value={newToDoTitle} on:keydown={addToDo}>

    <!-- Output -->
    {#each filteredTodos as todo}
        <div class="todo-item">
            <Todoitem {...todo} on:deleteTodo={handleDeleteTodo} on:toggleComplete={handleToggleComplete} />
        </div>
    {/each}

    <div class="inner-container">
        <div><label><input class="inner-container-input" type="checkbox" on:change={checkAllTodos}>Check All</label></div>
        <div>{todosRemaining} items left</div>
    </div>

    <div class="inner-container">
        <div>
            <button on:click={() => updateFilter('all')} class:active="{currentFilter === 'all'}">All</button>
            <button on:click={() => updateFilter('active')} class:active="{currentFilter === 'active'}">Active</button>
            <button on:click={() => updateFilter('completed')} class:active="{currentFilter === 'completed'}">Completed</button>
        </div>
        <div>
            <button on:click={clearCompleted}>Clear Completed</button>
        </div>
    </div>
</div>



<style>
   .logo {
       max-width: 100px;
       border-radius: 10px;
   }
</style>