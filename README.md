# INSEM-1
<!DOCTYPE html>
<html>
<head>
    <title>Register</title>
</head>

<body>

<h2>Create Account</h2>

<form method="POST">

    <input type="text"
        name="username"
        placeholder="Username"
        required>

    <br><br>

    <input type="password"
        name="password"
        placeholder="Password"
        required>

    <br><br>

    <button type="submit">Register</button>

</form>

<p>
    Already have an account?
    <a href="/login">Login</a>
</p>

</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <title>Task Management System</title>
</head>

<body>

<h2>Task Management System</h2>

<h3>Login</h3>

<form method="POST">

    <input type="text"
        name="username"
        placeholder="Username"
        required>

    <br><br>

    <input type="password"
        name="password"
        placeholder="Password"
        required>

    <br><br>

    <button type="submit">Login</button>

</form>

<p>
    Don't have an account?
    <a href="/register">Register</a>
</p>

</body>
</html>


<!DOCTYPE html>
<html>
<head>
    <title>Dashboard</title>
</head>

<body>

<h2>Task Management Dashboard</h2>

<p>Welcome, {{ username }}!</p>

<a href="/logout">Logout</a>

<hr>

<h3>Add New Task</h3>

<form action="/add_task" method="POST">

    <input type="text"
        name="title"
        placeholder="Task Title"
        required>

    <br><br>

    <textarea name="description"
            placeholder="Task Description"></textarea>

    <br><br>

    <label>Priority:</label>

    <select name="priority">

        <option value="Low">Low</option>
        <option value="Medium">Medium</option>
        <option value="High">High</option>

    </select>

    <br><br>

    <label>Deadline:</label>

    <input type="date" name="deadline">

    <br><br>

    <button type="submit">Add Task</button>

</form>

<hr>

<h3>My Tasks</h3>

{% if tasks %}

{% for task in tasks %}

<div>

    <h4>{{ task["title"] }}</h4>

    <p>{{ task["description"] }}</p>

    <p>
        Priority: <b>{{ task["priority"] }}</b>
    </p>

    <p>
        Deadline: {{ task["deadline"] }}
    </p>

    <p>
        Status: <b>{{ task["status"] }}</b>
    </p>

    <form action="/update/{{ task['id'] }}"
        method="POST">

        <select name="status">

            <option value="To Do"
                {% if task["status"] == "To Do" %}selected{% endif %}>
                To Do
            </option>

            <option value="In Progress"
                {% if task["status"] == "In Progress" %}selected{% endif %}>
                In Progress
            </option>

            <option value="Completed"
                {% if task["status"] == "Completed" %}selected{% endif %}>
                Completed
            </option>

        </select>

        <button type="submit">
            Update
        </button>

    </form>

    <br>

    <a href="/delete/{{ task['id'] }}">
        Delete Task
    </a>

</div>

<hr>

{% endfor %}

{% else %}

<p>No tasks available.</p>

{% endif %}

</body>
</html>
