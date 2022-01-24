---
title: Project Extra Credit
navbar: Guides
layout: guides
key: 5.2

tags:
  - text: 'New'
    type: 'is-primary'

---

This guide details extra credit opportunities that can be completed for projects 1, 2, and 3. Recall from the [syllabus](https://usfca.simplesyllabus.com/en-US/doc/63k541zg8/Fall-2021-CS-272-01-Software-Development?mode=view) that:

> Students may complete extra project functionality to make up for missing points. With the exception of the last search engine project, students may not earn more than 100% on any individual project. A list of extra credit options will be posted on the course website.

These extra credit opportunities can be completed to make up for points lost due to late penalties or other deductions.

See the [project 4b](project-4b.html) writeup for extra credit related to the final project.

## Eligibility
{: .page-header }

These extra credit opportunities are targeted towards students that are within a few percentage points of passing the course, but anyone that has received a non-zero project 1, 2, or 3 grade below 100% in Canvas may take advantage of these opportunities.

Extra credit may only be requested to make up for points missed on passing projects. These are projects for which you have passed functionality or code review (i.e. did not receive a partial grade), but missed points due to late penalties or other deductions.

For example, suppose you are fully passing project 1 and 2, but only received 50/100 points of project 3 functionality in your last code review. You may only earn extra credit for points lost on projects 1 and 2 in this case. If you lost 2 points on project 1 functionality and 5 points on project 2 design, you may earn up to 7 points of extra credit total. If you completed 10 points of extra credit options, the extra credit will be capped to 7 points instead (even if you lost points on project 3 as well). In this scenario, if you also want to earn extra credit on points lost for project 3, you must first work to pass all of the functionality tests first.

## Extra Credit
{: .page-header }

Below are some extra credit options. Each option is worth 5 points of extra credit.

  - **Javadoc:** Update and polish all of your Java documentation, then use the `javadoc` tool to generate a documentation website. Place the generated html in a [docs](https://github.blog/2016-08-22-publish-your-project-documentation-with-github-pages/) subfolder in your `main` branch. Ask the instructor or TA to enable Github Pages for your repository so that your documentation is viewable as a website.

  - **Driver Logic:** Reduce the duplicate logic in your `Driver` class for outputting data to a JSON file using lambda expressions.

  - **JSON and Stemming Logic:** Reduce the duplicate logic in your JSON writing and stemming classes using lambda expressions.

  - **Inverted Index Tests:** Create custom JUnit tests for your inverted index data structure. There should be 2 tests per public method (one for an empty index and one for a non-empty index) that do *not* expect exceptions, and at least 2 additional tests that expect an exception to be thrown.

  - **Custom Sorting**: Create a `Comparator` that will sort your custom search result object by score, total number of words in the file (instead of the number of matches), and then the path. Create test code to demonstrate this `Comparator` works. This test code can be a simple class with hard-coded arguments and console output; it does not need to be a unit test using JUnit.

  - **Verbose Flag**: Add a flag, `-verbose`, that enables logging `DEBUG` messages and above to the console. Add `DEBUG` messages before and after any file is read or written in the code, in every constructor call, and any time a thread is about to terminate. Create test code to demonstrate this feature works. This test code can be a simple class with hard-coded arguments and console output; it does not need to be a unit test using JUnit.

You are encouraged to ask for clarification on any of these you are interested in completing in a **public** anonymous post.

## Requests
{: .page-header }

You may request extra credit **exactly once**. You are encouraged to wait until the end of the semester to make a request.

After completing the extra credit, make a private post to the "Instructors" group with your request. The extra credit should already be completed; this is simply a request to have your grade updated in Canvas.

Include your name, a link *directly* to the extra credit feature(s), and the amount of extra credit you are requesting. **Be prepared to answer followup questions in a timely manner.**

See the [final code review](final-review.html) writeup for the deadline to complete extra credit.
