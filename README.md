index.html
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>LembreiFácil</title>

<style>
body {
  margin: 0;
  font-family: 'Segoe UI', sans-serif;
  background: linear-gradient(135deg, #4e73df, #1cc88a);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.container {
  background: white;
  width: 95%;
  max-width: 400px;
  padding: 25px;
  border-radius: 15px;
  box-shadow: 0 10px 25px rgba(0,0,0,0.2);
  text-align: center;
}

h1 {
  color: #4e73df;
}

input {
  width: 100%;
  padding: 12px;
  margin-top: 15px;
  border-radius: 8px;
  border: 1px solid #ccc;
}

button {
  width: 100%;
  padding: 12px;
  margin-top: 15px;
  border: none;
  border-radius: 8px;
  background-color: #4e73df;
  color: white;
  cursor: pointer;
  transition: 0.3s;
}

button:hover {
  background-color: #2e59d9;
}

ul {
  list-style: none;
  padding: 0;
  margin-top: 20px;
  text-align: left;
}

li {
  background: #f8f9fc;
  padding: 10px;
  border-radius: 8px;
  margin-bottom: 8px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.delete {
  background: red;
  color: white;
  border: none;
  border-radius: 5px;
  padding: 5px 8px;
  cursor: pointer;
}
</style>
</head>

<body>

<div class="container">
  <h1>LembreiFácil</h1>
  <p>Organize suas tarefas de forma simples e rápida.</p>

  <input type="text" id="tarefa" placeholder="Digite uma tarefa...">
  <button onclick="adicionarTarefa()">Adicionar</button>

  <ul id="lista"></ul>
</div>

<script>
let tarefas = JSON.parse(localStorage.getItem("tarefas")) || [];

function salvarTarefas() {
  localStorage.setItem("tarefas", JSON.stringify(tarefas));
}

function renderizarTarefas() {
  const lista = document.getElementById("lista");
  lista.innerHTML = "";

  tarefas.forEach((tarefa, index) => {
    const li = document.createElement("li");
    li.innerHTML = `
      ${tarefa}
      <button class="delete" onclick="removerTarefa(${index})">X</button>
    `;
    lista.appendChild(li);
  });
}

function adicionarTarefa() {
  const input = document.getElementById("tarefa");
  const texto = input.value.trim();

  if (texto === "") {
    alert("Digite uma tarefa!");
    return;
  }

  tarefas.push(texto);
  salvarTarefas();
  renderizarTarefas();
  input.value = "";
}

function removerTarefa(index) {
  tarefas.splice(index, 1);
  salvarTarefas();
  renderizarTarefas();
}

renderizarTarefas();
</script>

</body>
</html>
