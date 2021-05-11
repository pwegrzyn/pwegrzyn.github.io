---
authors:
- name: "Patryk Węgrzyn"
date: 2020-10-06
linktitle: Getting Started with OpenGL in 2020 
type:
- post 
- posts
title: Getting Started with OpenGL on Windows in 2020
weight: 1
categories:
- cpp
- graphics
- opengl
---

Picking up game development is pretty straightforward nowadays. You can just use one of the many beginner-friendly libraries/game-engines available in popular languages - for Python that would be
for example [PyGame](https://www.pygame.org/news), for Java - [FXGL](https://github.com/AlmasB/FXGL) and for JS - [GDevelop](https://gdevelop-app.com/). Or, if you want to dive straight into
more serious stuff, you could just go for [Unity](https://unity.com/). However, soon you'll notice that get more control over the graphics rendering pipeline (maybe you want to
squeeze every bit of performance of your game or you just wish to implement a cool graphics effect) there's currently still not better choice than picking good ol' C++ along with a low-level graphics library.

## Current GFX landscape

For a long time, rendering libraries were usually closely tied to the hardware that they were originally desinged to be run on. For example, if you wish to develop games on Windows you should definitely choose DirectX (or more
specifically - Direct3D). If you want to ship a game on Macs - go for Metal. Lately, a truly cross-platform API has been steadily been gaining more and more traction - Vulkan by Khronos. It's a really powerful, low-levelk framework
that promises to allow developing graphics-heavy apps on Windows, Mac and Linux. However, it has a considerable drawback from our perspective - it's not really beginner-friendly. Drawing a simple triangle on the screen would probably
require at least 500 lines of C++ and getting through hours of documentation and/or tutorials.

But fear not - there's one more cross-platform, powerful and respected graphics API - OpenGL. Yes, it's pretty old (30 years or so) and some of the design decisions made by the creators are questionable to say the least. But neverthless, it's still a very mature,
capable and more importantly - relatively easy to get started graphics rendering framework. Although the specification itself is pretty straightforward and simple - getting a running development setup might be a bit more tricky. That's what we'll cover next.

## Intro to OpenGL

First things first - OpenGL is not a library (nor a game engine), it's just an API specification - it's up to your hardware GPU mancufacturer to deliver their own implementation of the spec. If you use for example a NVIDIA card with up-to-date drivers, they will
most likely come with an full OpenGL implementation. On one hand this seems nice, becase we don't have to install the library manually, on the other hand - you will not have access to the source code, since it's proprietary (but then again, going through low-leve C code is not something most people would classify as enjoyable way of spending time). So, OpenGL itself will take care of that. Next, we need a way to create windows and handle interactions with them. This part is very OS-specific by it's nature. Technically, you would want to
just use your OS' API to handle all this stuff, but this approach is quite tedious and not portable. For a simple project a better way would be to use an existing windowing library. One of the best and easy-to-use in my opinion is [GLFW](https://www.glfw.org/). It's specifically desinged to work with OpenGL (and also OpenGL ES and Vulkan) and comes with support for Windows and Unix-like systems out of the box. So, just download the pre-compiled binaries for your OS and setup up static-linking in your IDE (many guids how to do that).

After that, you should be able to compile a simple program which creats a window within which you can later start rendering stuff. However, it will probably not link correctly. In order for it to link, you will need to include the ```openGL32.lib``` library in you linker dependencies. After doing so, it should work, but you'll quickly notice that the declarations of OpenGL functions are a bit weird. That's because we used the native Windows headers for OpenGL and they are not really up-to-date with modern OpenGL versions.

In order the you utilize the header declarations of more modern OpenGL functions we will use a library called [glew](http://glew.sourceforge.net/). It's job is to determine at run-time which extensions are available on your hardware, provide you with modern OpenGL declarations and finally do some magic behind-the-scenes to fetch the function pointers to the actual code delivered by your GPU manufacturer and map it the the aforementioned declarations. Getting started with using it might be a bit tricky so I'd advise you to just
follow the instructions on their page, since they are very informative and up-to-date.

Finally, after following all the steps above, you're ready to start writing OpenGL code.

## OpenGL API data abstractions in a nutshell

OpenGL's API, like many other graphics rendering APIs, follows a clear structure. In a typical rendering application you will have two major subsets of components - one for handling data and the other for handling the computations done on that data.
The main concept within the former group are *Vertex Buffer*. Think of those basically as smart data-arrays that automatically handle the process of pushing data into the GPU. VertexBuffer by itself are useless though, we first need a way to tell OpenGL
what is the structure of the data we put into the buffers. That's where *Vertex Attributes* come into play. They allow you to programatically specify what is the layout of the data and how should the GPU interpret it, byte-by-byte. *Vertex Attribute Pointers* are used
to bind attributes to buffers. In order to make the process more structured and manageable, OpenGL comes with what's known as *Vertex Arrays*. Technically, you could skip them entirely, and just a single, global, implicit array and do all the bindings why yourself, but
this quickly could become cumbersome, so the general advice is to use Vertex Arrays. The last major element of the data-focus-components are *Vertex Index Buffers*. They are used to re-use parts of the data you specified inside vertex buffers - specifically, instead of creating a huuge vertex buffer with the data for all the vertices of a complex 3D model you can just create a much simpler vertex buffer with only the main vertices and then later re-use the data associated with them via indices stored in index buffers.

## OpenGL processing bird's-eye view

That's the data-part of OpenGL, now let's swtich context a little bit and cover the other part of the pipeline - computations. You have all the data you want transfered beautifully to the GPU via vertex buffers, but how do you actually apply tranformations to the data (projections, texturing, lightning, etc.)? That's where *shaders* come into play. A *shader* is basically a separate sub-program within you application that is compiled and the run directly on the GPU. The two main categories of shaders we should be concerned for now are *vertex shaders* and *fragment shaders*. A typical rendering pipeline initiated by a draw call looks like this: the vertex shader is called for all vertices within you vertex buffer, and then the fragment shaders is called for all pixels that need to be displayed. Shaders are written in a DSL called OpenSL - it's a bit similar to C, but has some major differences that allow it to fit nicely within the aforementioned GPU processing pipeline. The are two major ways of passing data into shaders - uniforms and data specified within vertex buffers. The 
latter has already been covered, and the former - uniforms - are quite simple in nature, think of them as global variables avaiable within the context of both the CPU and GPU.

There are maaaany more interesting topics in OpenGL (textures, geometry shaders, all the maths behind projections, etc.) but I'll leave them for another post, since this was supposed to be a quick conceptual introduction :) 

Thanks for reading!