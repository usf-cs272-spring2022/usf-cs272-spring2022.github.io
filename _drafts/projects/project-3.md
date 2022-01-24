---
title: Project 3 Multithreading
navbar: Guides
layout: guides
key: 3.0
bump: false

assignments:
  - text: 'Project 3 Functionality'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118293'

  - text: 'Project 3 Design'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118299'
---

For this project, you will extend your [previous project](project-2.html) to support multithreading. In addition to meeting the previous project requirements, your code must make a thread-safe inverted index, and use work queues to build and search an inverted index using multiple threads.

## Functionality
{: .page-header }

The core functionality of your project must satisfy the following requirements:

  - Maintain the functionality of the [previous project](project-2.html).

  - Process **additional command-line parameters** to determine whether to use multithreading and if so, how many threads to use in the work queue. See the [Input](#input) section for specifics.

  - Support the **same output functionality** as before. See the [Output](#output) section for specifics.

  - Create a custom **read/write lock class** that allows multiple concurrent read operations. See below for specifics.

  - Create a new **thread-safe inverted index** using the custom read/write lock class above *in addition to* the original inverted index created for the previous projects.

  - Create a single **work queue with finish and shutdown** functionality. The work queue should not be initialized unless multithreading is enabled. See below for specifics.

  - Use the work queue to **support multithreaded building** the inverted index from a directory of files. Each worker thread should parse a single file.

  - Use the work queue to **support multithreaded searching** of the inverted index from a file of multiple word queries (for both exact and partial search). Each worker thread should handle an individual query line (which may contain multiple words).

  - Exit gracefully (shutting down all worker threads) *without* calling `System.exit()` when all of the building and searching operations are complete.

  - Extend your classes from previous projects or create completely new classes to support multithreading. **DO NOT REMOVE YOUR SINGLE THREADING CODE**, as you still need to support single threaded building and searching the index.

  - Do *NOT* use any of the classes in the `java.util.concurrent` package and do *NOT* use the `Stream.parallel` method for the multithreaded code.

The functionality of your project will be evaluated with various JUnit tests. Please see the [Testing](#testing) section for specifics.

### Simple Read/Write Lock

The custom simple read/write lock must support concurrent read operations, non-concurrent write and read/write operations, and allow an active writer to acquire additional read or write locks as necessary (i.e. reentrant write lock).

### Simple Work Queue

The work queue must support the ability to automatically track unfinished (or pending) work, and provide a method that waits until there is no more pending work. The work queue should also support the ability to shutdown gracefully.

**The work queue should not be initialized unless multithreading is enabled.** It is possible to reuse the same work queue for both building and searching if multithreading is enabled.

## Input
{: .page-header }

Your main method must be placed in a class named `Driver`. The `Driver` class should accept the following **additional** command-line arguments:

  - `-threads num` threads where `-threads` indicates the next argument `num` is the number of worker threads to use. If `num` is missing or an invalid number of threads are provided, please default to 5 threads.

    If the `-threads` flag is not provided, then a work queue should *not* be initialized and the project should execute *exactly* as previous projects.

The command-line flag/value pairs may be provided in any order, and the order provided is not the same as the order you should perform the operations (i.e. always build the index before performing search, even if the flags are provided in the other order).

Your code should support all of the command-line arguments from the [previous project](project-2.html) as well.

## Output
{: .page-header }

The output of your inverted index and search results should be the same from the [previous project](project-2.html). As before, you should **only generate output files if the necessary flags are provided**.

## Testing
{: .page-header }

Unlike previous projects, you only have to pass 100% of the tests in the `Project3aTest.java` group of JUnit tests to satisfy the project functionality requirements and sign up for your first project 3 code review. This test group does NOT include the long-running runtime tests that benchmark your single- versus multi-threading code.

This is handled automatically by the Github Actions test script. If it detects a project `v3.0.x` release it will automatically run `Project3aTest.java`. For all other releases, like `v3.1.x`, it will run `Project3bTest.java` instead. This DOES include the long-running runtime tests that benchmark your code. Be prepared to wait!

You must pass `Project3bTest.java` for followup code reviews and to earn the project design grade. This includes getting a speedup of at least `1.1x` faster on average using multi-threading. However, it is possible to get speedups of `1.7x` faster or more.

<article class="message is-warning">
  <div class="message-body"><i class="far fa-stopwatch"></i>&nbsp;Be patient. The tests for project 3 can take some time to complete, even if you have an efficient approach.</div>
</article>

## Related Content
{: .page-header }

The following content from this semester may be helpful in completing this project:

  - The `LoggerSetup` homework assignment demonstrates how to configure `log4j2` to debug code.

  - The `ReadWriteLock` homework assignment creates the simple read/write lock required by this project, and illustrates how to use it to make a data structure class thread-safe.

  - The `Synchronization` lecture code illustrates how to use a read/write lock to make a data structure class thread-safe.

  - The `PrimeFinder` homework assignment creates the work queue required by this project, as well as illustrates how to use a work queue and create tasks for non-recursive problems.

  - The `WorkQueues` lecture code illustrates how to use a work queue and create tasks for recursive problems. If your approach is not recursive, this example might not be helpful for this project.

  - The `WorkQueues` lecture code illustrates how to speed up multithreading code and avoid problems with over-blocking.

It is strongly recommended to pass all of the homework tests before integrating them into your projects.

## Hints
{: .page-header }

It is important to develop the project iteratively. One possible breakdown of tasks are:

  - Get `log4j2` working and start adding debug messages in your code. Once you are certain a class is working, disable debug messages for that class in your `log4j2.xml` file.

  - Consider extending your previous inverted index to create a thread-safe version. You may need to add additional functionality to your single-threaded versions.

  - Modify how you build your index to use multithreading and a work queue. Make sure you still pass the unit tests.

  - Modify how you search your index to use multithreading and a work queue. Make sure you still pass the unit tests.

  - Test your code in a multitude of settings and with different numbers of threads. Some issues will only come up occasionally, or only on certain systems.

  - Test your code with logging enabled, and then test your code with logging completely disabled. Your code will run faster without logging, which sometimes causes some concurrency problems.

  - Lastly, do not start on this project until you understand the multithreading code shown in class. If you are stuck on the code shown in class, PLEASE SEEK HELP. You do not need to figure it out on your own! You can ask the CS tutors, the teacher assistant, or the instructor for help.

**Do not worry about efficiency until after your first code review.** However, if you have had one code review and are running into issues, look for the following common issues:

  - Make sure the code does not over-notify (e.g. wake up threads more often than necessary).

  - Make sure the code does not over-finish (e.g. call finish more often than necessary).

  - Make sure the code does not over-block (e.g. perform blocking operations within a loop).

  - Make sure the code does not over-synchronize (e.g. preventing operations that could occur at the same time).

These issues are best detected using logging.

The important part will be to test your code as you go. The JUnit tests provided only test the entire project as a whole, not the individual parts. You are responsible for testing the individual parts themselves.
