# To-Do List App

Este é um projeto de aplicação de lista de tarefas (To-Do List) desenvolvido utilizando HTML, CSS e JavaScript.

## Descrição

A aplicação permite que os usuários adicionem, marquem como concluídas e removam tarefas. As tarefas são armazenadas no `localStorage` para que a lista permaneça intacta mesmo após recarregar a página.

## Funcionalidades

- **Adicionar Tarefas**: O usuário pode adicionar novas tarefas escrevendo no campo de texto e clicando no botão "Add".
- **Marcar Tarefas como Concluídas**: As tarefas podem ser marcadas como concluídas ao clicar nelas, aplicando uma estilização de risco sobre o texto.
- **Remover Tarefas**: O usuário pode remover tarefas clicando no ícone de "x" ao lado da tarefa.
- **Persistência de Dados**: As tarefas são salvas no `localStorage`, garantindo que a lista permaneça mesmo após o fechamento do navegador.

## Tecnologias Utilizadas

- **HTML**: Estrutura da aplicação.
- **CSS**: Estilização e layout da aplicação.
- **JavaScript**: Lógica da aplicação para adicionar, marcar e remover tarefas, além de salvar e recuperar dados do `localStorage`.

## Estrutura de Arquivos

```
├── images
│   ├── checked.png
│   ├── icon.png
│   └── unchecked.png
├── index.html
├── style.css
└── script.js
```
## Como Executar

1. Clone este repositório.
2. Abra o arquivo `index.html` em seu navegador.

## Imagens

Inclua as imagens necessárias na pasta `images` para o ícone e os estados das tarefas.

## Código CSS

```css
* {
    margin: 0;
    padding: 0;
    font-family: 'Poppins', sans-serif;
    box-sizing: border-box;
}
.container {
    width: 100%;
    min-height: 100vh;
    background: linear-gradient(135deg, #153677, #4e085f);
    padding: 10px;
}
.todo-app {
    width: 100%;
    max-width: 540px;
    background: #fff;
    margin: 100px auto 20px;
    border-radius: 10px;
    padding: 40px 30px 70px;
}
.todo-app h2 {
    color: #002765;
    display: flex;
    align-items: center;
    margin-bottom: 20px;
}
.todo-app h2 img {
    width: 30px;
    margin-left: 10px;
}
.row {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #edeef0;
    border-radius: 30px;
    padding-left: 20px;
    margin-bottom: 25px;
}
input {
    flex: 1;
    border: none;
    outline: none;
    background: transparent;
    padding: 10px;
    font-weight: 14px;
}
button {
    border: none;
    outline: none;
    padding: 16px 50px;
    background: #ff5945;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
    border-radius: 40px;
}
ul li {
    list-style: none;
    font-size: 17px;
    padding: 12px 8px 12px 50px;
    user-select: none;
    cursor: pointer;
    position: relative;
}
ul li::before {
    content: '';
    position: absolute;
    height: 28px;
    width: 28px;
    border-radius: 50%;
    background-image: url(images/unchecked.png);
    background-size: cover;
    background-position: center;
    top: 12px;
    left: 8px;
}
ul li.checked {
    color: #555;
    text-decoration: line-through;
}
ul li.checked::before {
    background-image: url(images/checked.png);
}
ul li span {
    position: absolute;
    right: 0;
    top: 5px;
    width: 40px;
    height: 40px;
    font-size: 22px;
    color: #555;
    line-height: 40px;
    text-align: center;
    border-radius: 50%;
}
ul li span:hover {
    background: #edeef0;
}
```

## Código JavaScript

```javascript
const inputBox = document.getElementById("input-box");
const listContainer = document.getElementById("list-container");

function addTask() {
    if (inputBox.value === '') {
        alert("You must write something!");
    } else {
        let li = document.createElement("li");
        li.innerHTML = inputBox.value;
        listContainer.appendChild(li);
        let span = document.createElement("span");
        span.innerHTML = "\u00d7";
        li.appendChild(span);
    }

    inputBox.value = "";
    saveData();
}

listContainer.addEventListener("click", function (event) {
    if (event.target.tagName === "LI") {
        event.target.classList.toggle("checked");
        saveData();
    }
    else if (event.target.tagName === "SPAN") {
        event.target.parentElement.remove();
        saveData();
    }
}, false);

function saveData() {
    localStorage.setItem("data", listContainer.innerHTML);
}

function showTask() {
    listContainer.innerHTML = localStorage.getItem("data");
}

showTask();
```

## Código HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To-Do List App</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <div class="todo-app">
            <h2>To-Do List <img src="images/icon.png" alt=""></h2>
            <div class="row">
                <input type="text" id="input-box" placeholder="Add your text">
                <button onclick="addTask()">Add</button>
            </div>
            <ul id="list-container">
                <!-- <li class="checked">Task 1</li>
                <li>Task 2</li>
                <li>Task 3</li> -->
            </ul>
        </div>
    </div>
    <script src="script.js"></script>
</body>
</html>
```
