---
title: Project Extra Credit
navbar: Guides
layout: guides
key: 5.1
bump: true

tags:
  - text: 'New'
    type: 'is-primary'

---

This guide details extra credit opportunities that can be completed for projects 1, 2, and 3. These extra credit opportunities can be completed to make up for points lost due to late penalties or other deductions.

Students that are eligible for the [Project 4b Search Engine](project-4b.html) project should complete the extra credit for that project instead.

## Eligibility
{: .page-header }

These extra credit opportunities are targeted towards students that are within a few percentage points of passing the course, but anyone that has received a non-zero project 1, 2, or 3 grade below 100% in Canvas may take advantage of these opportunities.

Extra credit may only be requested to make up for points missed on passing projects (passing both tests and code review). These are projects for which you already have a non-zero project final grade grade in Canvas.

For example, suppose you have non-zero final release grades for project 1 and 2, but only received 50/100 points of project 3 tests at the end of the semester. You may only earn extra credit for points lost on projects 1 and 2 in this case. If you lost 2 points on project 1 tests and 5 points on project 2 code review, you may earn up to 7 points of extra credit total. If you completed 10 points of extra credit options, the extra credit will be capped to 7 points instead (even if you lost points on project 3 as well). In this scenario, if you also want to earn extra credit on points lost for project 3, you must first work to pass all of the tests first.

## Extra Credit
{: .page-header }

Below are some extra credit options. Each option is worth 5 points of extra credit.

  - **Javadoc:** Update and polish all of your Java documentation, then use the `javadoc` tool to generate a documentation website. Place the generated html in a [docs](https://github.blog/2016-08-22-publish-your-project-documentation-with-github-pages/) subfolder in your `main` branch. Ask the instructor or TA to enable GitHub Pages for your repository so that your documentation is viewable as a website.

  - **Driver Logic:** Reduce the duplicate logic in your `Driver` class for outputting data to a JSON file using lambda expressions (but not stream pipelines).

  - **JSON Logic:** Reduce the duplicate logic in your JSON writing and stemming classes using lambda expressions (but not stream pipelines).

  - **Stemming Logic:** Reduce the duplicate logic in your stemming classes using lambda expressions (but not stream pipelines).

  - **Index Empty Tests:** Create custom JUnit tests for your inverted index data structure. There should be 1 test per public method that use an **empty** index and do *not* expect exceptions, and at least 1 additional test that expects an exception to be thrown.

  - **Index Non-Empty Tests:** Create custom JUnit tests for your inverted index data structure. There should be 1 test per public method that use a **non-empty** index and do *not* expect exceptions, and at least 1 additional test that expects an exception to be thrown.

  - **Custom Sorting**: Create a `Comparator` that will sort your custom search result object by score, total number of words in the file (instead of the number of matches), and then the path. Create test code to demonstrate this `Comparator` works. This test code can be a simple class with hard-coded arguments and console output; it does not need to be a unit test using JUnit.

  - **Verbose Flag**: Add a flag, `-verbose`, that enables logging `DEBUG` messages and above to the console. Add `DEBUG` messages before and after any file is read or written in the code, in every constructor call, and any time a thread is about to terminate. Create test code to demonstrate this feature works. This test code can be a simple class with hard-coded arguments and console output; it does not need to be a unit test using JUnit.

You are encouraged to ask for clarification on any of these you are interested in completing in a **public** anonymous post.

## Requests
{: .page-header }

You may request extra credit **exactly once**. You are encouraged to wait until the end of the semester to make a request.

After completing the extra credit, make a private post to the "Instructors" group with your request. The extra credit should already be completed; this is simply a request to have your grade updated in Canvas.

Include your name, links *directly* to the extra credit feature(s) in your code (do not just link to the repository---link to the exact branch, file, and lines of code), and the amount of extra credit you are requesting. **Be prepared to answer followup questions in a timely manner.**

See the [final code review](final-review.html) writeup for the deadline to complete extra credit.
