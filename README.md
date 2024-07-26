```markdown
# TODO Application

## Add Task

```html
<script>
    let alltasks = [];
    let list = document.getElementById("list");

    function add() {
        let task = document.querySelector("#task").value;
        if (task === "") {
            alert("Please add your task");
            return;
        }
        // Add task to the array
        alltasks.push(task);
        // Create a new task element
        let newelement = document.createElement("div");
        newelement.setAttribute("class", "eachtask");
        newelement.innerHTML = `
            <span><input type="checkbox" class="taskdone"></span>
            <span class="task">${task}</span>
            <span id="opButton">
                <button class="edit"><i class="fa-solid fa-pen-to-square"></i></button>
                <button class="delete"><i class="fa-solid fa-trash"></i></button>
            </span>`;
        list.appendChild(newelement);
        // Clear input field
        document.querySelector("#task").value = "";

        // Attach event listeners
        attachEventListeners(newelement);
    }

    function attachEventListeners(newelement) {
        // Attach delete event listener
        newelement.querySelector(".delete").addEventListener("click", function () {
            let currentelement = this.parentElement.parentElement;
            list.removeChild(currentelement);
        });

        // Attach checkbox change event listener
        newelement.querySelector(".taskdone").addEventListener("change", function (e) {
            let currentelement = this.parentElement.parentElement;
            if (e.currentTarget.checked) {
                currentelement.classList.add("eachtaskdone");
                currentelement.classList.remove("eachtask");
            } else {
                currentelement.classList.remove("eachtaskdone");
                currentelement.classList.add("eachtask");
            }
        });

        // Attach edit event listener
        newelement.querySelector(".edit").addEventListener("click", function () {
            let currentelement = this.parentElement.parentElement;
            let taskTextElement = currentelement.querySelector(".task");

            if (this.classList.contains("editing")) {
                let newInput = currentelement.querySelector(".newInput").value;
                taskTextElement.innerHTML = newInput;
                this.innerHTML = `<i class="fa-solid fa-pen-to-square"></i>`;
                this.classList.remove("editing");
            } else {
                let currentText = taskTextElement.textContent;
                taskTextElement.innerHTML = `<input type="text" value="${currentText}" class="newInput" autofocus/>`;
                this.innerHTML = "Save";
                this.classList.add("editing");
            }
        });
    }
</script>
```

## Delete Task

```html
<script>
    // Example: delete event listener for existing task elements
    // Make sure this code is executed when the new task element is created
    function attachEventListeners(newelement) {
        newelement.querySelector(".delete").addEventListener("click", function () {
            let currentelement = this.parentElement.parentElement;
            list.removeChild(currentelement);
        });
    }
</script>
```

## Mark Task as Complete/Incomplete

```html
<script>
    // Example: checkbox change event listener for existing task elements
    function attachEventListeners(newelement) {
        newelement.querySelector(".taskdone").addEventListener("change", function (e) {
            let currentelement = this.parentElement.parentElement;
            if (e.currentTarget.checked) {
                currentelement.classList.add("eachtaskdone");
                currentelement.classList.remove("eachtask");
            } else {
                currentelement.classList.remove("eachtaskdone");
                currentelement.classList.add("eachtask");
            }
        });
    }
</script>
```

## Edit Task

```html
<script>
    // Example: edit event listener for existing task elements
    function attachEventListeners(newelement) {
        newelement.querySelector(".edit").addEventListener("click", function () {
            let currentelement = this.parentElement.parentElement;
            let taskTextElement = currentelement.querySelector(".task");

            if (this.classList.contains("editing")) {
                let newInput = currentelement.querySelector(".newInput").value;
                taskTextElement.innerHTML = newInput;
                this.innerHTML = `<i class="fa-solid fa-pen-to-square"></i>`;
                this.classList.remove("editing");
            } else {
                let currentText = taskTextElement.textContent;
                taskTextElement.innerHTML = `<input type="text" value="${currentText}" class="newInput" autofocus/>`;
                this.innerHTML = "Save";
                this.classList.add("editing");
            }
        });
    }
</script>
```
