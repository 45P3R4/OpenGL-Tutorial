# Buffer arrays

- **VBO** - загружать данные в память GPU (вертексы, цвета, нормали)
- **EBO** - VBO, но он хранит индексы вершин


```C++
GLuint VBO;
//возвращает n неиспользуемых в настоящее время имен(id)
//Создания буферов здесь не происходит
glGenBuffers(1, &VBO);
//назначить буфер (на имя из прошлой команды) как активный
//Создания буферов здесь не происходит
glBindBuffer(GL_ARRAY_BUFFER, VBO);
    //передать данные по указаному адресу в текущий буфер вершин (VBO)
    //выделение памяти и загрузка данных в нее
    glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
//отвязать активный буфер (VBO)
glBindBuffer(GL_ARRAY_BUFFER, 0);

//..

//удалить буфер(обычно после главного цикла)
glDeleteBuffers(1, &VBO);
```


- **VAO** - какую часть VBO следует использовать в последующих командах

```C++
    GLuint VBO, VAO;
    glad_glGenVertexArrays(1, &VAO);
    glad_glGenBuffers(1, &VBO);
    
    glad_glBindVertexArray(VAO);

    glad_glBindBuffer(GL_ARRAY_BUFFER, VBO);
    glad_glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);

    //откуда брать данные для массива отрибутов и в каком формате
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 0, null);

    glad_glBindBuffer(GL_ARRAY_BUFFER, 0);
    glad_glBindVertexArray(0);
```

```C++
while(glfwWindowShouldClose(window) == GL_FALSE) {

    glBindVertexArray(VAO);
    //включает указанный vertex attribute array из первого аргумента glVertexAttribPointer()
    glEnableVertexAttribArray(0);
        //рисование примитивов  тип - начальная вершина - количество
        glDrawArrays(GL_TRIANGLES, 0, 3);
    //отключить аттрибуд для оптимизации(чтобы не было лишних передач данных в шейдеры)
    glDisableVertexAttribArray(0);
}
```
