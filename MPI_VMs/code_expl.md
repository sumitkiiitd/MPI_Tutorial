# MPI Hello World Application and Running an MPI Program

## Overview
- Basic MPI hello world application and running an MPI program.
- Intended for MPICH2 (1.4) installations.


### Code Excerpts
```cpp
#include <mpi.h>
#include <stdio.h>

int main(int argc, char** argv) {
    MPI_Init(NULL, NULL); // Initialize MPI environment

    int world_size;
    MPI_Comm_size(MPI_COMM_WORLD, &world_size); // Get number of processes

    int world_rank;
    MPI_Comm_rank(MPI_COMM_WORLD, &world_rank); // Get rank of the process

    char processor_name[MPI_MAX_PROCESSOR_NAME];
    int name_len;
    MPI_Get_processor_name(processor_name, &name_len); // Get processor name

    printf("Hello world from processor %s, rank %d out of %d processors\n",
           processor_name, world_rank, world_size); // Print message

    MPI_Finalize(); // Finalize MPI environment
}

```
## Key Functions

- **Initialize MPI**: 
    `MPI_Init(int* argc, char*** argv)`
  - Constructs MPI’s global and internal variables. The argc and argv parameters are used to pass command-line arguments to MPI. Passing NULL for both parameters means that the command-line arguments are not being passed to MPI. re’s why this might be done:

        1. Simplicity: If the MPI program does not need to process any command-line arguments, passing NULL makes the code simpler.
        2. Compatibility: Some MPI implementations allow NULL to be passed if command-line arguments are not needed. This ensures compatibility across different systems and MPI implementations.

- **Get Number of Processes**: 
    `MPI_Comm_size(MPI_Comm communicator, int* size)`
  - Returns the size of a communicator. In our example, MPI_COMM_WORLD (which is constructed for us by MPI) encloses all of the processes in the job, so this call should return the amount of processes that were requested for the job.



- **Get Rank of Process**: 
    `MPI_Comm_rank(MPI_Comm communicator, int* rank)`
  - Returns the rank of a process in a communicator. Each process inside of a communicator is assigned an incremental rank starting from zero. The ranks of the processes are primarily used for identification purposes when sending and receiving messages.

- **Get Processor Name**: 
    `MPI_Get_processor_name(char* name, int* name_length)`
  - Obtains the name of the processor on which process is executing.

- **Finalize MPI**: 
    `MPI_Finalize()`
  - Cleans up the MPI environment.
