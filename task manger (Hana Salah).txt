let tasks = [];
let currentFilter = "All";

function addTask() {
  const name = document.getElementById("taskName").value;
  const dueDate = document.getElementById("dueDate").value;
  const category = document.getElementById("category").value;

  if (name === "") return;

  tasks.push({
    name,
    dueDate,
    category
  });

  // Sort by due date
  tasks.sort((a, b) => {
    if (!a.dueDate) return 1;
    if (!b.dueDate) return -1;
    return new Date(a.dueDate) - new Date(b.dueDate);
  });

  document.getElementById("taskName").value = "";
  document.getElementById("dueDate").value = "";

  renderTasks();
}

function filterTasks(category) {
  currentFilter = category;
  renderTasks();
}

function renderTasks() {
  const taskList = document.getElementById("taskList");
  taskList.innerHTML = "";

  tasks
    .filter(task => currentFilter === "All" || task.category === currentFilter)
    .forEach(task => {
      const div = document.createElement("div");
      div.className = "task";
      div.innerHTML = `
        <strong>${task.name}</strong><br>
        <small>Category: ${task.category}</small><br>
        <small>Due: ${task.dueDate || "—"}</small>
      `;
      taskList.appendChild(div);
    });
}