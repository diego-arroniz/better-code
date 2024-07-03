# State

#### State

The State design pattern is one of the most widely used design patterns in the software development industry. The most popular JavaScript frameworks, such as React and Angular, rely heavily on the State pattern to manage application data and behavior based on that data.

In simple terms, the State design pattern is useful in situations where you can define definitive states of an entity (which could be a component, a page, an app, or a machine), and the entity has a predefined reaction to the state change.

Suppose you are trying to build a loan application process. Each step of the application process can be defined as a state.

While the customer usually sees a small list of simplified states of their application (pending, under review, approved, and rejected), there may be other internal steps involved. In each of these steps, the application will be assigned to a different person and may have unique requirements.

The system is designed so that at the end of processing in one state, it updates to the next one in line, and the next set of relevant steps begins.

Here's how to create a task management system using the State design pattern:

```javascript
javascriptCopy codeconst STATE_TODO = "TODO";
const STATE_IN_PROGRESS = "IN_PROGRESS";
const STATE_READY_FOR_REVIEW = "READY_FOR_REVIEW";
const STATE_DONE = "DONE";

function Task(title, assignee) {
    this.title = title;
    this.assignee = assignee;

    this.setAssignee = function (assignee) {
        this.assignee = assignee;
    };

    this.updateState = function (state) {
        switch (state) {
            case STATE_TODO:
                this.state = new TODO(this);
                break;
            case STATE_IN_PROGRESS:
                this.state = new IN_PROGRESS(this);
                break;
            case STATE_READY_FOR_REVIEW:
                this.state = new READY_FOR_REVIEW(this);
                break;
            case STATE_DONE:
                this.state = new DONE(this);
                break;
            default:
                return;
        }
        this.state.onStateSet();
    };

    this.updateState(STATE_TODO);
    function TODO(task) {
    this.onStateSet = function () {
        console.log(task.assignee + " notified about new task \"" + task.title + "\"");
    };
}

function IN_PROGRESS(task) {
    this.onStateSet = function () {
        console.log(task.assignee + " started working on the task \"" + task.title + "\"");
    };
}

function READY_FOR_REVIEW(task) {
    this.getAssignee = function () {
        return "Manager 1";
    };

    this.onStateSet = function () {
        task.setAssignee(this.getAssignee());
        console.log(task.assignee + " notified about completed task \"" + task.title + "\"");
    };
}

function DONE(task) {
    this.getAssignee = function () {
        return "";
    };

    this.onStateSet = function () {
        task.setAssignee(this.getAssignee());
        console.log("Task \"" + task.title + "\" completed");
    };
}

function run() {
    let task1 = new Task("Create a login page", "Developer 1");
    // Output: Developer 1 notified about new task "Create a login page"

    task1.updateState(STATE_IN_PROGRESS);
    // Output: Developer 1 started working on the task "Create a login page"

    let task2 = new Task("Create an auth server", "Developer 2");
    // Output: Developer 2 notified about new task "Create an auth server"

    task2.updateState(STATE_IN_PROGRESS);
    // Output: Developer 2 started working on the task "Create an auth server"

    task2.updateState(STATE_READY_FOR_REVIEW);
    // Output: Manager 1 notified about completed task "Create an auth server"
    task1.updateState(STATE_READY_FOR_REVIEW);
    // Output: Manager 1 notified about completed task "Create a login page"

    task1.updateState(STATE_DONE);
    // Output: Task "Create a login page" completed
    task2.updateState(STATE_DONE);
    // Output: Task "Create an auth server" completed
}

run();
```

Although the State pattern does a great job of segregating steps in a process, it can become extremely difficult to maintain in large applications that have multiple states.

Additionally, if your process design allows for something other than moving linearly through all the states, you will be forced to write and maintain more code since each state transition must be managed separately.
