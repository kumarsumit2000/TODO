```markdown
# TODO Application

## Add Task

```html
<script>
    let allTasks = [];
    function add() {
        let taskInput = document.querySelector("#taskInput").value;
        let list = document.querySelector("#list");
        if (taskInput == "") {
            alert("Please Enter Your Task !");
        } else {
            // Adding task to array
            allTasks.push(taskInput);
            //Creating task item
            let newTask = document.createElement("div");
            newTask.classList.add("eachtask");
            newTask.innerHTML = `<span><input type="checkbox" class="taskdone"></span>
            <span class="task">${taskInput}</span>
            <span id="opButton">
                <button class="edit"><i class="fa-solid fa-pen-to-square"></i></button>
                <button class="delete"><i class="fa-solid fa-trash"></i></button>
            </span>`;
            // Appending task in list
            list.appendChild(newTask);
            // Clear input field after append
            document.querySelector("#taskInput").value = "";
            //passing referance to delete function
            deletetask(newTask)
            //passing referance to taskCompleted function
            taskCompleted(newTask)
            //passing referance to editTask function
            editTask(newTask)
        }
        //Deletion operation
        function deletetask(newTask) {
            newTask.querySelector(".delete").addEventListener("click", function () {
                list.removeChild(newTask);
            })
        }

        //Completed operation
        function taskCompleted(newTask) {
            newTask.querySelector(".taskdone").addEventListener("change", function (e) {
                if (e.currentTarget.checked) {
                    newTask.classList.add("eachtaskdone");
                    newTask.querySelector(".taskdone").disabled = true;
                } else {
                    newTask.classList.remove("eachtaskdone");
                }

            })
        }

        //EditTask
        function editTask(newTask) {
            newTask.querySelector(".edit").addEventListener("click", function () {
                let textElement = newTask.querySelector(".task");
                let checking = newTask.querySelector(".taskdone");
                console.log(checking.checked)
                if (checking.checked) {
                    alert("Task already marked as completed");
                }
                else {
                    if (this.classList.contains("editing")) {
                        let newInput = newTask.querySelector(".newInput").value;
                        if (newInput == "") {
                            alert("Please update your task !!");
                        } else {
                            textElement.innerText = newInput;
                            this.innerHTML = `<i class="fa-solid fa-pen-to-square"></i>`;
                            this.classList.remove("editing")
                            alert("Task Updated");
                        }

                    } else {
                        this.classList.add("editing");
                        textElement.innerHTML = `<input type="text" value="${textElement.innerText}" class="newInput">`;
                        this.innerText = "Save";
                    }
                }


            })
        }


    }

</script>
```

## Delete Task
![Alt text](https://github.com/kumarsumit2000/NumberGuess/blob/main/Screenshot%202024-07-26%20204933.png)

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
![Alt text](https://github.com/kumarsumit2000/NumberGuess/blob/main/Screenshot%202024-07-26%20204833.png)

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
![Alt text](https://github.com/kumarsumit2000/NumberGuess/blob/main/Screenshot%202024-07-26%20204906.png)

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
