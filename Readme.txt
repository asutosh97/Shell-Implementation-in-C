Run the makefile to generate all executables.
On doing make, 3 executables are generated:
1.) server - corresponding to server.c
2.) shell - corresponding to client-shell.c
3.) get-one-file-sig - corresponding to get-one-file-sig.c

The descriptions are given below

server.c - this file contains a simple file server. The server forks off a new process for each client request and so, the server can handle multiple requests concurrently. Note that ideally the server should create a new thread for each incoming request. But, in the code, it rather forks off a new process. This has been done to show the aspects of multi-process programming.

get-one-file-sig.c - this file contains implementation of a simple client that can download one file from the server by sending the command: get <filename> to the server. The directory of file should be relative to the directory of the server.

client-shell.c - this file contains implementation of a "shell" which can execute several commands. Below is a list of commands the shell can execute:

1.) cd directoryname: simple cd command
2.) server server-IP server-port: store the server IP and port details for future file downloads
3.) getfl <filename>: download the file from the remote server and print its contents to the standard output. Note that this, and all future file download commands below, should have had a server IP address and port specified by the server command apriori; otherwise an error will be printed
4.) getfl filename > outputfile: download the file and store it in the specified filename
5.) getfl filename | command: causes the downloaded file contents to be piped to some built-in Linux command (like grep), and print whatever output comes out of the Linux command
6.) getsq file1 file2 file3 ...: download the multiple files sequentially, one after the other. Note that the file contents are discarded after download
7.) getpl file1 file2 file3 ...: download the multiple files in parallel, simultaneously. The next file download can, and will, start without waiting for the previous one to finish
8.) getbg filename: download the file in the background
9.) All simple built-in commands of Linux (like ls, cat, echo) etc. are supported
10.) exit: causes the shell to terminate, along with all child processes it has spawned
11.) Ctrl + C: terminates all foreground processes

Scope of improvement: The CPU usage is 100% when the server is running. This is because of the non blocking socket on which the server is listening. This can be changed so that the CPU usage is far less than 100%.