<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>DragonCodex</title>
  <style>
    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: #121212;
      color: #fff;
    }

    .login, .home, .editor {
      display: none;
      padding: 20px;
    }

    .active {
      display: block;
    }

    button {
      margin: 10px 5px;
      padding: 10px 15px;
      background: #fanta;
      border: none;
      cursor: pointer;
    }

    #output {
      background: #1e1e1e;
      padding: 10px;
      color: lime;
      margin-top: 10px;
    }

    textarea {
      width: 100%;
      height: 200px;
      background: #1e1e1e;
      color: #fff;
      border: 1px solid #333;
      padding: 10px;
    }
  </style>
</head>
<body>

<div class="login active" id="login">
  <h1>Welcome to DragonCodex</h1>
  <button onclick="login()">Login with Google</button>
  <button onclick="login()">Login with Facebook</button>
</div>

<div class="home" id="home">
  <h2>Your Projects</h2>
  <p id="projectList">No project</p>
  <button onclick="openEditor()">➕ New Project</button>
</div>

<div class="editor" id="editor">
  <textarea id="code" placeholder="Write HTML/JS code here..."></textarea><br>
  <button onclick="runCode()">▶ Run</button>
  <button onclick="stopCode()">■ Stop</button>
  <button onclick="saveProject()">💾 Save</button>
  <div id="output"></div>
</div>

<script>
  function login() {
    document.getElementById('login').classList.remove('active');
    document.getElementById('home').classList.add('active');
    loadProjects();
  }

  function openEditor() {
    document.getElementById('home').classList.remove('active');
    document.getElementById('editor').classList.add('active');
  }

  function runCode() {
    const code = document.getElementById('code').value;
    document.getElementById('output').innerHTML = code;
  }

  function stopCode() {
    document.getElementById('output').innerHTML = '';
  }

  function saveProject() {
    const name = prompt("Enter project name:");
    const code = document.getElementById('code').value;
    if (name) {
      localStorage.setItem(name, code);
      alert("Project saved!");
      loadProjects();
    }
  }

  function loadProjects() {
    const list = document.getElementById('projectList');
    if (localStorage.length === 0) {
      list.textContent = "No project";
    } else {
      let output = "<ul>";
      for (let i = 0; i < localStorage.length; i++) {
        const key = localStorage.key(i);
        output += `<li>${key}</li>`;
      }
      output += "</ul>";
      list.innerHTML = output;
    }
  }
</script>

</body>
</html>
