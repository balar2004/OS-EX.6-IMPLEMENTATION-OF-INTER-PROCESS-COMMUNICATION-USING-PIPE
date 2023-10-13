## OS-EX.6-IMPLEMENTATION-OF-INTER-PROCESS-COMMUNICATION-USING-PIPE
## INTER PROCESS COMMUNICATIONS
## Aim:
write C programs to illustrate IPC using pipes mechanisms
## Algorithm: IPC using pipes:
1. Create a child process usingfork()
2. Create a simple pipe with C, we make use of the pipe() systemcall.
3. Create two file descriptor fd[0] is set up for reading, fd[1] is set up forwriting
4. Close the read end of parent process using close() and perform writeoperation
5. Close the write end of child process and performreading
6. Display thetext.
## Program:
```
#include <stdio.h>
#include <unistd.h>
int main()
{
    int fd[2], child;
    char a[10];
    printf("Enter the string:");
    scanf("%s", a);
    if (pipe(fd) == -1)
    {
        perror("Pipe creation failed");
        return 1;
    }
    child = fork();
    if (child == -1)
    {
        perror("Fork failed");
        return 1;
    }
    if (!child)
    {
        close(fd[0]);
        write(fd[1], a, 5);
    } 
    else
    {
        close(fd[1]);
        read(fd[0], a, 5);
        printf("The string received from the pipe is: %s\n", a);
    }
    return 0;
}
```
## Output:

## Result:
Thus, IPC using pipes mechanisms is illustrated using c program successfully.
