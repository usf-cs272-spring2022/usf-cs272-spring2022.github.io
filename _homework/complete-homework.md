---
layout: guides
navbar: Guides
title: Completing Homework
key: 2
---

This guides discusses how to work on your homework and submit it for grading.

## Modifying Homework Code
{: .page-header }

Refer to the `TODO` comments in the template code for specifics on what code to fill in or modify for the assignment. When modifying this code, keep in mind the following:

  - **Do not modify any method or class declarations.** For example, you cannot add or remove keywords like `static` or add a `throws` keyword to a method if one was not already included.

  - **Do not modify methods that are already fully defined.** For example, if a method is provided and has no `TODO` comments within the method definition, you may not modify that method.

  - **Do not modify the test code.** This includes any input or output files utilized by the test code.

  - You MAY add additional members and methods as needed to the code.

  - You MAY add additional classes and imports for those classes as long as they are a part of core Java or one of the pre-approved third-party libraries (Apache OpenNLP, Apache Commons Text, Apache Log4j2, Jetty, MariaDB).

  - You MAY add comments to clarify code for yourself. You can add comments to already defined methods if you want.

  - You MAY change a `return` statement in a method with a `TODO` comment as needed. (You may *not* change the return type in the method declaration, however.)

  - Remove the `TODO` comments when you are done. This removes them from the "Tasks" view in Eclipse. If you want to keep the comment around, you can change the text `TODO` to `DONE` instead.

Post on [Piazza]({{ site.data.info.links.forums.link }}) if you have any questions regarding what must be done for a homework assignment or a question about your homework grade.

## Receiving Homework Credit
{: .page-header }

To receive full credit on any homework assignment, you must:

  - **Pass all of the unit tests remotely.** See the [Testing Homework](/guides/homework/test-homework.html) guide detailed steps. You will not receive full points if you are passing the tests locally but not remotely.

  - **Commit your work often.** Some assignments require a minimum number of commits! Consider making a commit after you complete every `TODO` in the code or after you pass a new test. <i class="fas fa-star has-text-warning"></i>

  - **Avoid warnings.** Some assignments require the code to compile with no warnings to earn full points. Try to make sure your code is warning-free in Eclipse before testing your code remotely!

  - **Follow the `TODO` directions.** For example, if the `TODO` comment stated you must use a `HashSet` and your code does not, you could lose points even if you are passing all of the unit tests.

  - **Properly submit your homework on time.** By default, Github Classroom will report your grade based on the last commit *before* the deadline and will ignore all other commits after that. You will have to reach out on Piazza to have late submissions regraded manually.

To submit your homework, you must make a commit and push that commit to Github before the deadline!
