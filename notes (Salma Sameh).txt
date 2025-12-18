const saveBtn = document.getElementById("saveNoteBtn");
const titleInput = document.getElementById("noteTitle");
const contentInput = document.getElementById("noteContent");
const notesList = document.getElementById("notesList");

saveBtn.addEventListener("click", function () {
  const title = titleInput.value.trim();
  const content = contentInput.value.trim();

  if (title === "" || content === "") {
    alert("Please enter both a title and content.");
    return;
  }

  const noteDiv = document.createElement("div");
  noteDiv.classList.add("note");   // 

  const noteTitle = document.createElement("h4");
  noteTitle.textContent = title;

  const noteText = document.createElement("p");
  noteText.textContent = content;

  noteDiv.appendChild(noteTitle);
  noteDiv.appendChild(noteText);

  notesList.appendChild(noteDiv);

  titleInput.value = "";
  contentInput.value = "";
});
