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

1. ## Creating Classes in C
    > The following style of C coding is a technique I've adapted from [cirocosta](https://github.com/cirocosta/observer-c) via github.  Despite the fact that inheritance is still not an option, I find that developing your C code in the following manner helps with keeping an organized name space, preventing redundant code, and producing a less convoluted main function. Note that the following convention has nothing to do with SDL directly and only serves as a great vehicle to implement GUI programs with the graphics library.

   - ### my_class.h
        > Starting with *my_class.h*, we can see that we are declaring our prototypes within a block of preprocessor directives. Defining `#ifndef` ensures that the declarations which follow it, until defining `#endif`, will only be declared once, thus preventing a linker error.

        ```c
        #ifndef MY_CLASS_H
        #define MY_CLASS_H

        typedef struct _my_class
        {
            void (*destroy)(struct _my_class *this);
            void (*print)(struct _my_class *this);
            const char * str;
        } my_class;

        my_class *CREATE_MY_CLASS(const char * str);

        #endif /* MY_CLASS_H */
        ```

        > The typedef declaration prototypes a structure `_my_class` as a named type `my_class`. The leading underscore is a naming convention that I've adopted which, as you will see in the future, will give us a more readable namespace. There are two variables declared as function pointers(`destroy` and `print`.) Note that actual function prototypes can not be declared within a typedef declaration. Feel free to add any C primitives that you will need access to via your class. Last we declare a function which returns a pointer to your class obj, It might be helpful for you to think of this as the constructor for your class.

   - ### my_class.c
        > In the *.c* file we define a set of static functions that match the function pointers we declared previously.  These are the functions that the function pointers will point too.  Take note of the leading underscores, such that...
        
        > `void (*destroy)(struct _my_class *this)` in *.h*, will point to `static void _destroy(my_class *this)` in *.c*.
        
        
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
        static void _print(my_class *this)
        {
            printf("%s\n", this->str);
        }

        /* Allocated memory for object */
        my_class *CREATE_MY_CLASS(const char * str)
        {
            my_class *this = malloc(sizeof(*this));
            this->destroy = _destroy;
            this->print = _print;
            this->str = str;

            return this;
        }
        ```

        > Define the *constructor* method which allocates a pointer(*this*) to your class.
        
        > Assign the declared function pointers to their corresponding function and return the class object pointer.

    - ### main.c
        > Now in main, create an instance of the class object, and call the print function.
        
        ```c
        #include <stdio.h>
        #include <stdlib.h>
        #include <string.h>
        #include "my_class.h"

        int main(int argc, char **argv)
        {
            my_class *hello_obj = CREATE_MY_CLASS("HelloWorld!");
            hello_obj->print(hello_obj);
            hello_obj->destroy(hello_obj);

            my_class *goodbye_obj = CREATE_MY_CLASS("GoodbyeWorld!");
            goodbye_obj->print(goodbye_obj);
            goodbye_obj->destroy(goodbye_obj);

            return 0;
        }
        ```

        > Free your pointer with the *destroy* method.

    > The ability to create multiple objects of the same type that share the same functions and primitives; lets the C coder implement and understand C in a few ways.

      1. Avoid functions with an awkward number of parameters my passing the object instead
      2. Return multiple variables.
      3. Gain a stronger understanding of function pointers.
      4. Avoid memory leaks by encapsulating allocation and de-allocation methods.

    > Using this convention will help a coder realize why `C++` and `Java` were created and gain an appreciation for the people who created them.  As for SDL, keeping logic and graphics rendering separated is now an option, among other things.




2. ## Delta Time

    <img class="ui medium left floated image" src="../images/delta.png">

    > A novice programmer will be eager create graphics, and that's okay. Just remember, for implementing anything more complex than rendering a single frame to the screen, delta time is required. Creating a method that returns delta time is key in ensuring that SDL doesn't fry your cpu.  Running a game loop without delta is equivalent to the following C code.

    ```c
    int main(int argc, char ** argv)
    {
        while(1)
            ;
        return 0;
    }
    ```

    > Many online sources over complicate delta time; and for good reason as there are numerous implementations that vary. I hope that with respect to simplicity, the following function explains one variation delta time quite well.


    ```c
    int main(int argc, char ** argv)
    {
        unsigned int IPS = 1;   /* Iterations per second */
        while(1) {
            /* render */
            /* now do something */
            sleep(IPS);
        }
        return 0;
    }
    ```

    > This particular variation being, if you want to your code to do something every *x* seconds when, wait for *x* seconds, then do something. Animation in general requires a frame to be rendered 60 times every second thus delta time can be calculated as follows.

    ```java
    time_per_tick :=       // calculate how much time each loop iteration should take to achieve 60 fps
    ticks_per_second :=    // calculate how many ticks per second with respect to time per tick
    timer := 0             // most likely wil be nano seconds
    ticks := 0            
    time_now := 0
    time_before := 0
    frames_rendered := 0

    while(running)
        time_now := // function that returns time since epoch
        timer := time_now - time_before
        ticks := ticks + timer
        time_before := time_now
        render() //render a frame
        frames_rendered ++
        logic()  //perform logic
        if(timer < time_per_tick)
            delay(time_per_tick - timer)  // see SDL_Delay
        if(ticks > ticks_per_second)
            ticks := 0
            print(frames_rendered)
            frames_rendered := 0
    ```

    > One could argue that this implementation is not an implementation of delta time such that a lot of methods calculate delta time such that 

    ```java
    delta_time:
    while(running)
        delta_time := calculate_delta()
        if(delta_time > 1)
            render()
        logic()
    ```

    > In this instance rendering only happens when it is needed to achieve FPS such that...
    
    > ` (delta exists in R(1,...infinity) --> render graphics) execute game logic`
    
    > Hence, the game logic is executing on every tick.

    > As a code base grows a common problem is that you are rendering to few frames per second. Unless frame dropping logic is implemented, animation can appear delayed.  Simple programs can be costly such as an implementation of *Conways Game of Life* where each cell is the size of one pixel. In my implementation, which is featured later, the cell size can be adjusted, thus if I set the size to one pixel, my program will have to loop through a 2D array of size `1000 x 1000` on every tick in order to perform the game logic and upgrade the canvas.

    > Otherwise low frame rate should not occur in small projects and should be a warning that something in the code base is taking way longer than it should. A common mistake is that the programmer has not implemented their code such that the rendering and logic are separate. See the pseodocode as follows...

    ```c
    int game(Sprite *sprite, Renderer *renderer)
    {
        if(sprite->faces_left(sprite)) {
            render(renderer, sprite->left_frame(sprite, renderer));
        }
        else if(sprite->faces_right(sprite)) {
            render(renderer, sprite->right_frame(sprite, renderer));
        }
        // etc...
    }
    ```
    
    > The latter displays numerous problems, in SDL you want to avoid passing the renderer into functions that take it out of the scope of main. A different way to say this is, avoid surrounding render calls with conditional. One frame may contain a lot of textures that all need to be rendered to the canvas separately. The cleanest way to implement this is to render all your textures one after the other. This is not easy to do such that, the textures, coordinates, and properties ...etc of a game object will be encapsulated within the object.  The following section was the way I dealt with this problem.

2. ## Writing My Own Render Queue