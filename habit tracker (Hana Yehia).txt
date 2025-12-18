const taskInput = document.getElementById("taskInput");
const dateInput = document.getElementById("dateInput");
const saveBtn = document.getElementById("saveBtn");
const taskList = document.getElementById("taskList");

let tasks = [];

// Button click
saveBtn.addEventListener("click", addTask);

function addTask() {
  const name = taskInput.value.trim();
  const date = dateInput.value;

  if (name === "") {
    alert("Please enter a task name");
    return;
  }

  tasks.push({
    name,
    date,
    completed: false
  });

  // Sort by due date
  tasks.sort((a, b) =>
    (a.date || "9999") > (b.date || "9999") ? 1 : -1
  );

  taskInput.value = "";
  dateInput.value = "";

  renderTasks();
}

function toggleTask(index) {
  tasks[index].completed = !tasks[index].completed;
  renderTasks();
}

function renderTasks() {
  taskList.innerHTML = "";

  tasks.forEach((task, index) => {
    const taskDiv = document.createElement("div");
    taskDiv.className = "task";

    taskDiv.innerHTML = `
      <input type="checkbox" ${task.completed ? "checked" : ""}>
      <div class="${task.completed ? "completed" : ""}">
        <div class="task-name">${task.name}</div>
        <div class="task-date">
          ${task.date ? "Due Date: " + formatDate(task.date) : ""}
        </div>
      </div>
    `;

    taskDiv.querySelector("input")
      .addEventListener("click", () => toggleTask(index));

    taskList.appendChild(taskDiv);
  });
}

function formatDate(date) {
  const [y, m, d] = date.split("-");
  return `${d}/${m}/${y}`;
}
