Html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>ToDo List</title>
    <link rel="stylesheet" href="style.css">
</head>

<body>
    <header>
        <h1>ToDo List</h1>
    </header>

    <main>
        <form autocomplete="off">
            <label>
                <input id="new-todo" name="todo" type="text" placeholder="new todo" />
            </label>
            <select id="user-todo" name="user">
                <option disabled selected>select user</option>
            </select>
            <button>Add Todo</button>
        </form>
        <ul id="todo-list"></ul>
    </main>
    
    <script src="app.js"></script>
</body>

</html>


Ts
type ID = string | number;

interface Todo {
    userId: ID,
    id: ID,
    title: string,
    completed: boolean
}

interface User {
    id: ID,
    name: string,
}

(function () {
    const todoList = document.getElementById('todo-list');
    const userSelect = document.getElementById('user-todo');
    const form = document.querySelector('form');
    let todos: Todo[] = [];
    let users: User[] = [];

    //Attach Events
    document.addEventListener('DOMContentLoaded', initApp);
    form?.addEventListener('submit', handleSubmit);

    //Basic Logic
    function getUserName(userId: ID){
        const user = users.find((u) => u.id ===userId);
        return user?.name || '';
    }
    function printTodo ({ id, userId, title, completed}: Todo) {
        const li =document.createElement('li');
        li.className = 'todo-item';
        li.dataset.id  = String(id);
        li.innerHTML = `<span>${title} <i>by</i> <b>${getUserName(
            userId
        )}</b></span>`;

        const status = document.createElement('input');
        status.type = 'checkbox';
        status.checked = completed; 
        status.addEventListener('change', handleTodoChange);

        const close = document.createElement('span');
        close.innerHTML = '';
        close.className = 'close';
        close.addEventListener('click', handleClose);

        li.prepend(status);
        li.append(close);

        todoList?.prepend(li);
    }

    function createUserOption(user: User) {
        if (userSelect) {
            const option = document.createElement('option');
            option.value = String(user.id);
            option.innerText = user.name;
    
            userSelect.append(option);
        }

        }
     

    function removeTodo(todoId: ID) {
        if (todoList) {
            todos = todos.filter((todo) => todo.id !== todoId);

            const todo = todoList.querySelector(`[data-id="${todoId}"]`);
            if (todo){
                
            todo.querySelector('input')?.removeEventListener('change', handleTodoChange);
            todo.querySelector('.close')?.removeEventListener('click', handleClose);
    
            todo.remove();
            }
        }
    }

    function alertError(error: Error) {
        alert(error.message);
    }

    //Event Logic
    function initApp() {
        Promise.all([getAllTodos(), getAllUsers()]).then((values) =>{
            [todos,users] = values;

            todos.forEach((todo) => printTodo(todo));
            users.forEach((user) => createUserOption(user));
        });
    }
    
    function handleSubmit(event: Event) {
        event.preventDefault();

        if(form){
            createTodo({
                userId: Number(form.user.value),
                title: form.todo.value,
                completed: false,
            });
        }
    }

    function handleTodoChange (this: HTMLInputElement) {
        const parent = this.parentElement
        if (parent){
            const todoId = parent.dataset.id;
            const completed = this.checked;
    
            todoId && toggleTodoComplete(todoId, completed);
        }
       
}
function handleClose (this: HTMLSpanElement){
    const parent = this.parentElement

    if (parent){
        const todoId = parent.dataset.id;
        todoId && deleteTodo(todoId);
    }
    
}

//Async Logic
async function getAllTodos(): Promise<Todo[]> {
    try {
        const response = await fetch(
            'https://jsonplaceholder.typicode.com/todos?_limit=15'
        );
        const data = await response.json();

        return data;   
    } catch (error){
        if (error instanceof Error)
          alertError(error);  
        
        return [];
    }
}

async function getAllUsers(): Promise<User[]> {
    try {
        const response = await fetch(
            'https://jsonplaceholder.typicode.com/users?_limit=5'
        );
        const data = await response.json();

        return data;
    }   catch (error) {
        if (error instanceof Error)
          alertError(error);

        return [];
        
    }
}

async function createTodo(todo: Omit<Todo, 'id'>) {
    try{
        const response = await fetch(
            'https://jsonplaceholder.typicode.com/todos',
            {
                method: 'POST',
                body: JSON.stringify(todo),
                headers: {
                    'Content-Type': 'application/json',
                },
            }
        );

        const newTodo = await response.json();

        printTodo(newTodo);
    }   catch (error) {
        if (error instanceof Error)
          alertError(error);
    }
}

async function toggleTodoComplete(todoId: ID, completed: boolean) {
    try {
        const response = await fetch(
            `https://jsonplaceholder.typicode.com/todos/${todoId}`,
            {
                method: 'PATCH',
                body: JSON.stringify({ completed }),
                headers: {
                    'Content-Type': 'application/json',
                },
            }
        );

        if (!response.ok) {
            throw new Error('Failed to connect with the server! Please try later.');
        }
    } catch (error) {
        if (error instanceof Error)
          alertError(error);
    }
}
  
async function deleteTodo(todoId: ID) {
    try{
        const response = await fetch(
            `https://jsonplaceholder.typicode.com/todos/${todoId}`,
            {
              method: 'DELETE',
              headers: {
                'Content-Type': 'application/json',
              },     
            }
        );

        if (response.ok) {
            removeTodo(todoId);
        } else {
            throw new Error('Failed to connect with the server! Please try later.');
        }
    } catch (error) {
        if (error instanceof Error)
          alertError(error);
    }
}
})()

CSS
* {
    box-sizing: border-box;
}
body {
    margin: 0;
    font-size: 1.2rem;
}
header {
    background-color: rgb(73, 12, 12);
    color: rgb(247, 229, 229);
    height: 100px;
    padding: 2rem 1rem;
    text-align: center;
}
h1 {
    font-family: Arial, Helvetica, sans-serif;
    margin: 0;
}
form {
    width: 500px;
    margin: 2rem auto;
    display: flex;
    flex-direction: column;
    gap: 1rem;
}
form input, form select {
    padding: 0.5rem 1rem;
}
input[type="text"] {
    width: 100%;
}
form > button {
    cursor: pointer;
    background-color:  rgb(73, 12, 12);
    color: white;
    border: none;
    padding: 0.5rem 0.8rem;
}
form > button:hover {
    background-color: rgb(0, 0, 0);
}

ul {
    list-style: none;
    width: 500px;
    margin: 2rem auto;
    padding: 0;
}

.todo-item {
    display: flex;
    gap: 1rem;
    padding: 0.5rem 0;
}
.close {
    color: red;
    cursor: pointer;
    font-weight: bolder;
}
.close:hover {
    color:tomato
}

  
