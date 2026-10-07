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

print("--- Initializing Pipes ---");

// 2. Instantiate individual, isolated pipe objects using the factory constructor
var pipe1 = pipe();
var pipe2 = pipe();

// 3. Open processes/commands in read-only mode
// (These run concurrently and keep their handles isolated internally)
var status1 = pipe1.open("echo Hello from Pipe 1!");
var status2 = pipe2.open("bonezegei -v");

if (status1 == 0 || status2 == 0) {
print("Failed to open one or more pipes.");
}

// 4. Read and process stream output from Pipe 1
print("\n--- Reading from Pipe 1 ---");
var line1 = pipe1.getline();
while (line1 != 0) {
  // Trim trailing newline if needed
  var size = sizeof(line1);
  
  if (size > 0) {
    line1[size - 1] = " "; // strip the newline character
  }

  print("[Pipe 1 Output]: " + line1);
  line1 = pipe1.getline();
}

// Close the first pipe stream and free its internal handle
pipe1.close();
```
The example demonstrates how to use pipe_open and pipe_getline from the Bonezegei
 Scripting Language Pipe library to perform inter-process communication by capturing the
 output of external commands. The pipe_open function launches a specified executable
 (like "bonezegei–info" or "bonezegei-v") and returns a pipe object that connects to its
 output stream. This stream is then read line by line using pipe_getline, which retrieves
 each line until the end of the output is reached (signaled by a return value of 0). The
 code also trims the trailing newline from each line for cleaner display, allowing the script
 to process and print the output of external commands in a structured, readable format.
