# Brief History of MPI

## Pre-1990s
- Writing parallel applications for different computing architectures was difficult and tedious.
- Many libraries could facilitate building parallel applications, but there was no standard accepted way of doing it.
- Most parallel applications were in the science and research domains.

## Message Passing Model
- Commonly adopted by libraries at the time.
- An application passes messages among processes to perform a task.
- Examples:
  - A manager process assigns work to worker processes by passing a message describing the work.
  - A parallel merge sorting application sorts data locally on processes and passes results to neighboring processes to merge sorted lists.
- Almost any parallel application can be expressed with the message passing model.

## Supercomputing 1992 Conference
- Authors of libraries and others came together to define a standard interface for message passing.
- The goal was to create the Message Passing Interface (MPI) standard.
- This standard would:
  - Allow programmers to write parallel applications portable to all major parallel architectures.
  - Enable the use of familiar features and models from popular libraries.

## MPI-1 (1994)
- A complete interface and standard was defined by 1994.
- MPI is only a definition for an interface; developers needed to create implementations for their architectures.
- Complete implementations of MPI became available by 1995.
- MPI was widely adopted and continues to be the de-facto method for writing message-passing applications.
