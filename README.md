### Bonezegei Scripting Language Library: Pipe

The BSL_pipe library provides an essential and intuitive mechanism for Inter-Process Communication (IPC) within the Bonezegei Scripting Language environment. It introduces the concept of a unidirectional data channel (a pipe), allowing the output stream of one process or function to be seamlessly channeled as the input stream to another, executing processes in a sequential, stream-based manner.

### Install using Package Installer
<strong>Note</strong> Go to the directory where the .bzg script is located 

* Windows cmd 
    ``` bash 
    bzg install pipe
    ```
* Linux Terminal
    ``` bash
    sudo bzg install pipe
    ``` 

### Usage
This code show how to use the pipe functions
``` js
//Include the pipe library
include("lib/pipe.bzg");

//pipe_open(<executable>) 
var pipe1 = pipe_open("bonezegei --info");
var pipe2 = pipe_open("bonezegei -v");

print("\nReading from Pipe1...");  // pipe_getline(<the pipe>)
var line = pipe_getline(pipe1);    // Reads the output stream of the executable
while (line != 0) {

    // This code removes the extra new line
    var size = sizeof(line);      
    line[size - 1] = " ";     
    
    print("Pipe1: " + line);
    line = pipe_getline(pipe1);
}

print("\nReading from Pipe2...");
var line = pipe_getline(pipe2);
while (line != 0) {

    var size = sizeof(line);
    line[size - 1] = " "; 

    print("Pipe2: " + line);
    line = pipe_getline(pipe2);
}

```