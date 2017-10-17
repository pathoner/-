# 评论框
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>新的功能</title>
        <style>
        .done {
            color: gray;
            text-decoration: line-through;
        }
        </style>
    </head>
    <body>
        <div class="todo-form">
            <input id = "id-input-todo">
            <button id = "id-button-add">Add</button>
        </div>
        <div id ="todo-div-container">
            <!-- <div class="todo-cell done">
                <button class="todo-done">完成</button>
                <button class="todo-delete">删除</button>
                <span contenteditable="true">11</span>
            </div> -->
        </div>
    </body>
</html>
<script>
// 创建一个数组用来保存localStorage中的数据
var yyear = []
// 先解析
yyear = JSON.parse(localStorage.years)
var datefunction = function() {
        var date = new Date();
        var year =  date.getFullYear()
        var month = date.getMonth() + 1
        var day = date.getDate()
        var hours = date.getHours()
        var minutes = date.getMinutes()
        var Y_m_d = `${year}/${month}/${day} ${hours}:${minutes}`
        // 日期对象的一个储存
        yyear.push(Y_m_d)
        // 存储在localStorage.years 中
        localStorage.years = JSON.stringify(yyear)
        // 然后解析

        console.log(localStorage.years)
}
datefunction()


    var log = function() {
        console.log.apply(console, arguments)
    }
    var insertTodo = function(todo) {
        var todoContainer = e('#todo-div-container')
        var t = templateTodo(todo)
        todoContainer.insertAdjacentHTML("beforeend", t)
    }
    var e = function(selector) {
        return document.querySelector(selector)
    }
    // var templateTodo = function(todo) {
    //     var t = `
    //         <div class='todo-cell'>
    //             <button class='todo-done'>完成</button>
    //             <button class='todo-delete'>删除</button>
    //             <span contenteditable='true'>${todo}</span>
    //         </div>
    //     `
    //     return t
    // }
    // var todos = []
    // todos = JSON.parse(localStorage.simpletodos)
    // for(var i = 0; i < todos.length; i++) {
    //     var t = todos[i]
    //     insertTodo(t)
    var todos = []
    var loadTodos = function() {
        // var todos = []
        todos = JSON.parse(localStorage.simpletodos)
        for(var i = 0; i < todos.length; i++) {
            var t = todos[i]
            insertTodo(t)
        }
    }
     //
    // var insertTodo = function(todo) {
    //     var todoContainer = e('#todo-div-container')
    //     var t = templateTodo(todo)
    //     todoContainer.insertAdjacentHTML("beforeend", t)
    // }
    // var e = function(selector) {
    //     return document.querySelector(selector)
    // }

    var addButton = e('#id-button-add')
    addButton.addEventListener("click", function(event){
        var todoInput = e("#id-input-todo")
        var todo = todoInput.value
        // var todoContainer = e('#todo-div-container')
        // var t = templateTodo(todo)
        // todoContainer.insertAdjacentHTML("beforeend", t)
        insertTodo(todo)
        todos.push(todo)
        localStorage.simpletodos = JSON.stringify(todos)
        // e("#id-div-todo-container").innerHTML = ""


    })
    var templateTodo = function(todo) {
        var t = `
            <div class='todo-cell'>
                <button class='todo-done'>完成</button>
                <button class='todo-delete'>删除</button>
                <span contenteditable='true'>${todo}</span>

            </div>
        `
        return t
    }
    var todoContainer = e('#todo-div-container')
    todoContainer.addEventListener("click", function (event) {
        //  log('container click', event, event.target)
        var target = event.target
        if(target.classList.contains("todo-done")) {
            // log("done")
            var todoDiv = target.parentElement
            toggleClass(todoDiv, 'done')
        } else if (target.classList.contains("todo-delete")) {



            var button = event.target
            log("button是什么",button)
            var cell = button.parentElement
            log("cell是什么", cell)
            var cells = cell.parentElement.children
            log("cells是什么", cells)
            var index = 0
            for(var i = 0; i < cells.length; i++) {
                var c = cells[i]
                if(c == cell) {
                    index = i
                    break
                }
            }
            // log("xiabiao", index)

            todos.splice(index, 1)
            localStorage.simpletodos = JSON.stringify(todos)
            var todoDiv = target.parentElement
            todoDiv.remove()
        }
    })

    var toggleClass = function(element, className) {
        if(element.classList.contains(className)) {
            element.classList.remove(className)
        } else {
            element.classList.add(className)
        }
    }
loadTodos()
</script>
