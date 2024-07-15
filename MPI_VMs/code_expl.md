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

## Key Functions

- **Initialize MPI**: `MPI_Init(int* argc, char*** argv)`
  - Constructs MPI’s global and internal variables.

- **Get Number of Processes**: `MPI_Comm_size(MPI_Comm communicator, int* size)`
  - Returns the size of a communicator.

- **Get Rank of Process**: `MPI_Comm_rank(MPI_Comm communicator, int* rank)`
  - Returns the rank of a process in a communicator.

- **Get Processor Name**: `MPI_Get_processor_name(char* name, int* name_length)`
  - Obtains the name of the processor.

- **Finalize MPI**: `MPI_Finalize()`
  - Cleans up the MPI environment.
