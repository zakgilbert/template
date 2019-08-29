---
layout: project
type: project
image: images/c_logo.png
title: A 2D Game Engine
permalink: projects/SDL2
# All dates must be YYYY-MM-DD format!
date: 2019-08-28
labels:
  - SDL2
  - The C Programming Language
  - Graphics Library
  - Pong
  - Conways Game of Life
  - Cellular Automata
  - JRPG
  - Render Queue
  - Font Atlas
summary: A look at my personal endeavors with SDL2 and the C programming language. 
---
<img class="ui small right floated image" src="../images/SDL_Logo.svg.png">

The Simple Directmedia Layer or [SDL](https://www.libsdl.org/) has been the plight of my coding life for the past year. As most new programmers do, I too yearned to write my own 2D game.  I chose a graphics library built for C because I enjoy C and I saw it as a fun way to gain coding experience. After a year, the result is a small library the allows one to write a simple 2D game in a relatively short amount of time. The following accounts highlight the problems I encountered and the results the spawned as I solved these problems.

## Creating Classes in C

The following style of C coding is a technique I've adapted from [cirocosta](https://github.com/cirocosta/observer-c) via github.  Despite the fact that inheritance is still not an option, I find that developing your C code in the following manner helps with, keeping an organized name space, preventing redundant code, and producing a less convoluted main function. 

- ### my_class.h
    
    > Starting with *my_class.h* we can see that we are defining our prototypes within a block of preprocessor directives. Defining `#ifndef` ensures that the declarations which follow it, until defining `#endif`, will only be declared once, thus preventing a linker error.
    
    ```c
    #ifndef MY_CLASS_H
    #define MY_CLASS_H

    typedef struct _my_class
    {
        void (*destroy)(struct _my_class *this);
        void (*print)(struct _my_class *this, const char *str);
    } my_class;

    my_class *CREATE_MY_CLASS();

    #endif /* MY_CLASS_H */
    ```

    > The typedef declaration defines a structure `_my_class` as a named type `my_class`. The leading underscore is a naming convention that I've adopted which, as you will see in the future, will give us a more readable namespace. There are two variables defined as function pointers(`destroy` and `print`.) Note that actual function prototypes can not be defined within a typedef declaration. Feel free to add any C primitives that you will need access to via your class. Last we define a function which returns a pointer to your class obj, It might be helpful for you to think of this as the constructor for your class.

- ### my_class.c
    
    > Moving on to the C file

    ```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    #include "my_class.h"

    /* Free allocated memory */
    static void _destroy(my_class *this)
    {
        if (NULL != this) {
            free(this);
            this = NULL;
        }
    }

    /* print a string with newline */
    static void _print(my_class *this, const char *str)
    {
        printf("%s\n", str);
    }

    /* Allocated memory for object */
    my_class *CREATE_MY_CLASS()
    {
        my_class *this = malloc(sizeof(*this));
        this->destroy = _destroy;
        this->print = _print;

        return this;
    }
    ```

- ### main.c

    ```c
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>
    #include "my_class.h"

    int main(int argc, char **argv)
    {
        my_class *my_class_obj = CREATE_MY_CLASS();
        my_class_obj->print(my_class_obj, "Hello World!");
        my_class_obj->destroy(my_class_obj);

        return 0;
    }
    ```


### Delta Time

<img class="ui medium left floated image" src="../images/delta.png">
