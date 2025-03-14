
# Простая отрисовка

```
glClearColor(0.2, 0.2, 0.2, 1);
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

        glLoadIdentity(); //Загрузить единичную матрицу
        glScalef(0.5, 0.5, 0.5); //Размер матрицы
        glRotatef(45, 0, 0, 1); //Вращение матрицы
        glTranslatef(0.5, 1, 1); //Перемещение матрицы

        glBegin(GL_TRIANGLES);
            glColor3f(1, 0, 0); glVertex2f(0, 0);
            glColor3f(0, 1, 0); glVertex2f(0.5, 0);
            glColor3f(0, 0, 1); glVertex2f(0, 0.5);
        glEnd();
```

# Отрисовка с массивами

## Массивы

```    
    POINTFLOAT vertices[] = {
        {-1, -1},
        {-1, 1},
        {1, 1},
        {1, -1}
    };

    float colors[] = {1,0,0, 0,1,0, 0,0,1, 1,1,0};

    GLuint index[] = {1,2,3};
```

## Отрисовка

```
        glClearColor(0.2, 0.2, 0.2, 1);
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

        glVertexPointer(2, GL_FLOAT, 0, &vertices); 
        glEnableClientState(GL_VERTEX_ARRAY); //Подключение массива вертексов

        glColorPointer(3, GL_FLOAT, 0, &colors);
        glEnableClientState(GL_COLOR_ARRAY); //Подключение массива цветов

            glDrawElements(GL_TRIANGLES, 3, GL_UNSIGNED_INT, &index); //Рисование по индексам

        glDisableClientState(GL_VERTEX_ARRAY);
        glDisableClientState(GL_COLOR_ARRAY);
```

если нужно нарисовать все вершины, вместо ```glDrawElements()``` нужно написать ```glDrawArrays(GL_TRIANGLE_FAN, 0, 4);```

- Задать перспективную проекцию ```glFrustum(-1,1, -1,1, -1,5);```
- Включить буфер глубины ```glEnable(GL_DEPTH_TEST);```
