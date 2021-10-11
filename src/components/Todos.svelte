<script>
    import Todoitem from './Todoitem.svelte';

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


//Check if user checks checkbox then... reset
function checkAllTodos(event){
    todos.forEach(todo => todo.completed = event.target.checked);
    todos = todos;
}

function updateFilter(newFilter){
    currentFilter = newFilter;
}

function clearCompleted() {
    todos = todos.filter(todo => !todo.completed);
}

// Check and filter out if id property not present then remove 
function handleDeleteTodo(event) {
    todos = todos.filter(todo => todo.id !== event.detail.id)
}

//Toggle if completed or not completed by checking is ID in todos index array is included/Find in detail property of event object 
function handleToggleComplete(event) {
    const todoIndex = todos.findIndex(todo => todo.id === event.detail.id)
    const updatedTodo = { ...todos[todoIndex], completed: !todos[todoIndex].completed};

// Building new array with uncompleted todos, copy array and slice 0-todoIndex
    todos = [ ...todos.slice(0, todoIndex),
            updatedTodo,
            ...todos.slice(todoIndex+1)
            ];
}
</script>


<div class="container">
    <img src={'./images/flagAfrica.png'} alt="Flags of African countries in African continent" class="logo">
    
    <h2>To Do App</h2>
    <input type="text" class="todo-input" placeholder="Insert to-do item" bind:value={newToDoTitle} on:keydown={addToDo}> -->

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
    h2 {
		color: rgb(174, 43, 226);;
		text-transform: uppercase;
		font-size: 2em;
		font-weight: 100;
	}
    .logo {
        max-width: 100px;
        border-radius: 10px;
    }
    .container {
        max-width: 800px;
        margin: 10px auto;
    }
    .todo-input {
        width: 100%;
        padding: 1-px, 20px;
        font-size: 18px;
        margin-bottom: 20px;
    }
    .inner-container {
        display: flex;
        align-items: center;
        justify-content: space-between;
        font-size: 16px;
        border-top: 1px solid lightgreen;
        padding-top: 15px;
        margin-bottom: 15px;
    }
    .inner-container-input {
       margin-right: 12px;
    }
    button {
        font-size: 14px;
        background-color: white;
        appearance: none;
    }
    button:hover {
        background: lightseagreen;
    }
    button:focus {
        outline: none;
    }
    .active {
        background: lightseagreen;
    }
 </style>
