## Bare-bones opengl setup for vscode windows

The given code is a working example but you should set it up yourself so you are familiar with the process.

Prerequisite downloads:
- Download GLFW windows pre-compiled x64 binaries from https://www.glfw.org/download.html.
- Follow instructions "Setting up GLAD" from https://learnopengl.com/Getting-started/Creating-a-window. 
- Follow instructions at https://code.visualstudio.com/docs/cpp/config-mingw#_prerequisites to download MSYS2 and adding C:\msys64\mingw64\bin to your PATH.

Files you need from glfw and glad folders you downloaded:
- glfw-\<current-version>.bin.WIN64/include/glfw3.h
- glfw-\<current-version>.bin.WIN64/include/glfw3native.h
- glfw-\<current-version>.bin.WIN64/lib-mingw-w64/glfw3.dll
- glfw-\<current-version>.bin.WIN64/lib-mingw-w64/libglfw3dll.a
- glad/include/glad/glad.h
- glad/include/KHR/khrplatform.h
- glad/src/glad.c

You also need main.cpp from /src/main.cpp in this project.

Setup up your workspace directory to look like the following:   
{workspaceFolder}/
- include/
   -  glad/
      - glad.h
   - GLFW/
      - glfw3.h
      - glfw3native.h
   - KHR/
      - khrplatform.h
- lib/
   - libglfw3dll.a
- src/
   - glad.c
   - main.cpp
- glfw3.dll

Follow the rest of the instructions at https://code.visualstudio.com/docs/cpp/config-mingw#_prerequisites for setting up:

- .vscode/
    - tasks.json (build instructions)
    - launch.json (debugger settings)

Make sure you read the parts that teach how to:
- build (ctrl-shift-B)
- build and run without debugging (ctrl-F5)
- build and debug (F5)

Alter the args in tasks.json to be:
```json
"args": [
    "-g",
    "-std=c++17",
    "-I${workspaceFolder}/include",
    "-L${workspaceFolder}/lib",
    "${workspaceFolder}/src/*.cpp",
    "${workspaceFolder}/src/glad.c",
    "-lglfw3dll",
    "-o",
    "${workspaceFolder}/app.exe"
],
```

Doing ctrl-F5 should render a rectangle to a opengl window.
