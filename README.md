# To_do_list
document.addEventListener("DOMContentLoaded", loadTasks);

function addTask() {
    let taskInput = document.getElementById("taskInput");
    let taskText = taskInput.value.trim();
    if (taskText === "") return;
    let taskList = document.getElementById("taskList");
    let li = document.createElement("li");
    li.textContent = taskText;
    li.addEventListener("click", () => {
        li.classList.toggle("completed");
        saveTasks();
    });
    let deleteBtn = document.createElement("button");
    deleteBtn.textContent = "Delete";
    deleteBtn.className = "delete-btn";
    deleteBtn.addEventListener("click", () => {
        taskList.removeChild(li);
        saveTasks();
    });
    li.appendChild(deleteBtn);
    taskList.appendChild(li);
    taskInput.value = "";
    saveTasks();
}

function saveTasks() {
    let tasks = [];
    document.querySelectorAll("#taskList li").forEach((task) => {
        tasks.push({ text: task.firstChild.textContent, completed: task.classList.contains("completed") });
    });
    localStorage.setItem("tasks", JSON.stringify(tasks));
}

function loadTasks() {
    let tasks = JSON.parse(localStorage.getItem("tasks")) || [];
    let taskList = document.getElementById("taskList");
    tasks.forEach((taskData) => {
        let li = document.createElement("li");
        li.textContent = taskData.text;
        if (taskData.completed) {
            li.classList.add("completed");
        }
        li.addEventListener("click", () => {
            li.classList.toggle("completed");
            saveTasks();
        });
        let deleteBtn = document.createElement("button");
        deleteBtn.textContent = "Delete";
        deleteBtn.className = "delete-btn";
        deleteBtn.addEventListener("click", () => {
            taskList.removeChild(li);
            saveTasks();
        });
        li.appendChild(deleteBtn);
        taskList.appendChild(li);
    });
}



body {
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 0;
}

nav {
    background: #070707;
    color: rgb(255, 255, 255);
    padding: 10px;
}

nav ul {
    list-style: none;
    display: flex;
    justify-content: space-around;
}

nav a {
    color: white;
    text-decoration: none;
}

section {
    padding: 20px;
    margin: 20px 0;
}

.profile-pic {
    width: 150px;
    border-radius: 50%;
}

.project {
    margin: 20px 0;
}

.project img {
    width: 100%;
    height: auto;
}

form {
    display: flex;
    flex-direction: column;
}

form input, form textarea {
    margin: 10px 0;
    padding: 10px;
}

button {
    background: #0ae96e;
    color: white;
    border: none;
    padding: 10px;
    cursor: pointer;
}

button:hover {
    background: #f8f545;
}

/* Responsive Design */
@media (max-width: 600px) {
    nav ul {
        flex-direction: column;
    }
}
