��#   T O D O 

#Add Task

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

</script>

#delete Task

<script>
   // Attach delete event listener to the new delete button
        newelement.querySelector(".delete").addEventListener("click", function () {
            let currentelement = this.parentElement.parentElement;
            list.removeChild(currentelement);
        });
</script>

#on Complete Task
<script>
 //  on check box click
        newelement.querySelector(".taskdone").addEventListener("change", function (e) {
            let currentelement = this.parentElement.parentElement;
            let taskText = currentelement.querySelector("span:nth-child(2)").textContent;
             // task done
            if (e.currentTarget.checked) {
                currentelement.classList.add("eachtaskdone");
                currentelement.classList.remove(".eachtask");
            } 
            // task pending
            else{
                currentelement.classList.remove("eachtaskdone");
                currentelement.classList.add("eachtask");
            }

        });
        // end of checkbox
</script>

#Edit Task

<script>
       // Adding event listener to the Edit button
newelement.querySelector(".edit").addEventListener("click", function () {
    let currentelement = this.parentElement.parentElement;
    let taskTextElement = currentelement.querySelector("span:nth-child(2)");
   
    // Check if we are currently in edit mode
    if (this.classList.contains("editing")) {
        // Save the new task text
        let newInput = currentelement.querySelector(".newInput").value;
        taskTextElement.innerHTML = newInput;
        this.innerHTML = `<i class="fa-solid fa-pen-to-square"></i>`;
        this.classList.remove("editing");
    } else {
        // Switch to edit mode
        let currentText = taskTextElement.textContent;
        taskTextElement.innerHTML = `<input type="text" value="${currentText}" class="newInput" autofocus/>`;
        this.innerHTML = "Save";
        this.classList.add("editing");
    }
});
</script>
 
