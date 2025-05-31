#html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>To-Do List with Time & Checkbox</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <h1>My To-Do List</h1>
    <input type="text" id="taskInput" placeholder="Add new task...">
    <button onclick="addTask()">Add</button>
    <ul id="taskList"></ul>
  </div>
  <script src="script.js"></script>
</body>
</html>

#css
body {
  font-family: Arial, sans-serif;
  background-color: #1e1e1e; /* Dark background */
  color: white;
  display: flex;
  justify-content: center;
  padding-top: 50px;
}

.container {
  background-color: #2c2c2c; /* Dark container */
  padding: 20px;
  border-radius: 10px;
  width: 320px;
  box-shadow: 0 0 10px #000;
}

input[type="text"] {
  width: 65%;
  padding: 8px;
  margin-right: 5px;
  background-color: #3a3a3a;
  border: none;
  color: white; /* white text */
  border-radius: 5px;
}

button {
  padding: 8px 10px;
  border: none;
  border-radius: 5px;
  background-color: #E0A1B7;
  color: white;
  cursor: pointer;
}

ul {
  list-style-type: none;
  padding: 0;
  margin-top: 20px;
}

li {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #3d3d3d;
  padding: 10px;
  margin-bottom: 10px;
  border-radius: 5px;
}

li span {
  flex: 1;
  margin-left: 10px;
  color: white;
}

.time {
  font-size: 0.8em;
  color: #aaa;
  margin-left: 10px;
}

button.edit {
  background-color: #4AAEB6;
  color: white;
}

button.delete {
  background-color: #AF1E23;
  color: white;
  margin-left: 5px;
}

input[type="checkbox"] {
  transform: scale(1.2);
  accent-color: #E0A1B7; /* Tick in black */
}

#js
function addTask() {
  const input = document.getElementById("taskInput");
  const taskText = input.value.trim();
  if (taskText === "") return;

  const li = document.createElement("li");

  const checkbox = document.createElement("input");
  checkbox.type = "checkbox";

  const span = document.createElement("span");
  span.innerText = taskText;

  const dateSpan = document.createElement("span");
  dateSpan.className = "time";
  const now = new Date();
  dateSpan.innerText = `${now.toLocaleDateString()} ${now.toLocaleTimeString()}`;

  const editBtn = document.createElement("button");
  editBtn.innerText = "Edit";
  editBtn.className = "edit";
  editBtn.onclick = () => {
    const newTask = prompt("Edit task:", span.innerText);
    if (newTask !== null && newTask.trim() !== "") {
      span.innerText = newTask.trim();
    }
  };

  const delBtn = document.createElement("button");
  delBtn.innerText = "Delete";
  delBtn.className = "delete";
  delBtn.onclick = () => li.remove();

  li.appendChild(checkbox);
  li.appendChild(span);
  li.appendChild(dateSpan);
  li.appendChild(editBtn);
  li.appendChild(delBtn);

  document.getElementById("taskList").appendChild(li);
  input.value = "";
}
