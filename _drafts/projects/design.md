---
title: Project Design
navbar: Guides
layout: guides
key: 0.4

#tags:
#  - text: 'Updated'
#    type: 'is-info'

assignments:
  - text: 'Project 1 Design'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118297'
    info: '(<a href="project-1.html">Writeup</a>)'

  - text: 'Project 2 Design'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118298'
    info: '(<a href="project-2.html">Writeup</a>)'

  - text: 'Project 3 Design'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118299'
    info: '(<a href="project-3.html">Writeup</a>)'

  - text: 'Project 4 Design'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118300'
    info: '(<a href="project-4b.html">Writeup</a>)'

---

Each project grade is split into two components: functionality (passing tests) and design (passing code review). This guide details the process for getting credit for project design.

## Types

 We use expert code reviews with the instructor to evaluate your project design. There are two types of code reviews:

  - **Synchronous:** This is the default type of code review. These code reviews are 20 minute synchronous appointments conducted via Zoom. You do not need to enable video during these appointments, but you must enable audio.

      **You may have at most one synchronous appointment per week.** The first code review for each project will *always* be synchronous. Projects usually require at least 2 synchronous code reviews.

      *If you are concerned that you do not have the technology requirements for a synchronous discussion, email the instructor and your CASA advisor asking about accommodation options.*

  - **Asynchronous:** These are code review requests that will be completed by the instructor asynchronously. You do not need to sign up for a code review appointment.

      **You must be pre-approved by the instructor to request this type of code review.** Asynchronous requests are only pre-approved if your code only needs minor changes to pass.

By default, you should request a **synchronous** code review appointment unless directed otherwise by the instructor.

## Eligibility

Before making a code review request, you should make sure you are eligible:

  - Do you have a non-zero functionality grade for the **current** project?

      *For example, if you want a design grade for project 2, you must already have a non-zero functionality grade for project 2 in Canvas.*

  - Do you have a non-zero design grade of the **previous** project?

      *For example, if you are on project 2, you must already have a non-zero design grade for project 1. If you are on project 1, you can skip this check.*

  - Have you **cleaned up your code** for review? See the "Preparation" section below for details.

      *This includes making sure it is well-formatted, uses proper naming conventions, is well-documented, compiles free of warnings, handles exceptions properly, and does not have any left-over debug code.*

  - Do you have a **current release** for this project that passed the functionality tests?

      *The instructor will only review functional code. You must pass these tests before every single code review.*

  - Are there **0 commits** to your `main` branch since your release? You can check for commits on the releases page:

      ![Screenshot]({{ "/images/github-release-with-change.png" | relative_url }}){: .is-400 }

      *If you have made changes to your `main` branch, create a new release with the latest changes before requesting review. We need to know the code being reviewed passes the tests!*

  - Was your previous synchronous appointment **last week** or earlier?

      *You can request at most one synchronous code review appointment per week. This does not guarantee an appointment per week! If you request an appointment late in the week, it is unlikely you will get one that week.*

      *You can skip this check if you are requesting an asynchronous code review.*

If you answered yes to all of the above, you can request a code review to have your project design evaluated. You need to verify eligibility before *every* code review.

## Deadlines

The design grade is based on the **pull request reviewed date** of the **first** approved code review on Github. This is *not* when the code review was requested, nor the date of the passing release. It is the date when the code was **first** reviewed by the instructor (i.e. the date of your code review appointment), not the date your code actually passes code review. However, the grade will remain 0 until code review is passed.

There is a **5% late deduction per 72 hours** that the project design is late. For example, the design grade will be 95% if the first passing release is between 1 minute to 3 day late. There is another one-time **5% late deduction** if you have more than a ~~10 day~~ **14 day** gap in between code reviews.

Projects require between 2 to 5 code reviews to pass. On average, expect to require the following number of code reviews:

| Project | Synchronous | Asynchronous |
|:--------|:-----------:|:------------:|
| 1, Inverted Index | 3+ | 1+ |
| 2, Partial Search | 2+ | 1+ |
| 3, Multithreading | 2+ | 1+ |
| 4, Search Engine  | 1* | 0* |
{: style="width: auto;" }

_*The last search engine project is only code reviewed once during finals week. Partial grades will be assigned during that time._ See the [Schedule](schedule.html) for the other design deadlines.

<i class="fas fa-exclamation-triangle"></i> **New:** The late penalty will be capped at 30% maximum. If your project is significantly late, you will still be able to earn a **70%** functionality grade (assuming no other deductions).
{: .notification .is-success }

## Preparation

Before your functional code will be reviewed by the instructor, you need to work on the following:

  - Your code should follow [proper code style and naming conventions](/guides/eclipse/configuring-eclipse.html#code-formatting). Check your code format (or run the built-in formatter in Eclipse). Double-check your variable names, method names, and class names.

  - Your code should be professionally documented using Javadoc notation. This includes well-written descriptions of every method and class with no missing Javadoc tags.

  - Your code should have no warnings, including Javadoc warnings.

      There are two ways to check this locally. First, [configure Eclipse to show you warnings](../eclipse/configuring-eclipse.html). Second, you can [run using the Maven command](/guides/projects/project-testing.html#running-maven) to see the exact warnings that will be found by the Github Actions script.

  - Your code should have no old `TODO` comments and `main` methods outside of the `Driver` class. Do not forget to check for these in any homework classes you decide to use for your project!

  - Your code should not produce user-friendly error output and not print any stack traces to the console.

  - Your code should not have any commented-out code. Delete commented out code before requesting code review.

It is highly likely you need to cleanup your code before each code review, even if your code is already passing the functionality tests.

## Design

During the code review, the instructor will be checking that your code is professional and production-ready. In addition to the preparation outlined above, this includes making sure that:

  - Your code is professionally written (e.g. code style, naming, documentation).
  - Your code is object-oriented.
  - Your code is properly encapsulated.
  - Your code is generalized and reusable.
  - Your code is memory and time efficient (within reason).
  - Your code is user-friendly and handles exceptions properly.
  - Your code handles resources properly.

This list is not exhaustive and exactly what we look for will vary by project.

**The design of your code should be your own.** The point of code review is to help you gain practice and intuition refactoring and redesigning your code. That only works if we are working from YOUR design.

During appointments, the instructor will rarely ask you to explain how your code works. Instead, the instructor will ask you *why* you chose to approach design a certain way. The answer should *never* be "because someone told me to do it this way."

Keep in mind code reviews are more about **training** than assessment. There is no expectation you know how to apply the design principles discussed in class to your code at the start of the process. In fact, your projects should start out poorly-designed... otherwise you may be in the wrong class!

## Requests

Use the "Request Code Review" action to request a code review. Specifically:

  1. Make sure you are eligible for code review. The action will verify some, but not all, of the eligibility requirements.

  1. Click on "Request Code Review" under the "Actions" tab.

  1. Click the "Run workflow" button. This button is next to the text, "This workflow has a workflow_dispatch event trigger."

      a. Enter the project release, e.g. `v1.0.0`, that passed the tests.

      b. Enter `s`, `sync`, or `synchronous` to indicate you are requesting a synchronous code review, or `a`, `async`, or `asynchronous` to request an asynchronous code review.

      c. Keep the dropdown on the `main` branch. Code reviews will *always* be conducted from the `main` branch.

  1. Wait for the action to finish running. When it is complete, click the "Request Code Review" link until you see the run details.

  1. If the run was successful, click the link to visit the draft pull request that was created. If everything worked properly, the pull request should be assigned to a teacher assistant, have the `project#` and request type labels, and belong to the `Project #` milestone (where `#` is a project number). It should also have information about your project release and past requests.

  1. Follow the instructions on the pull request. When done, click the "Ready to Review" button.

  1. Wait 2 business days. If you have not heard a response by then, double check your pull request is not in draft mode and reach out privately on [CampusWire]({{ site.data.info.links.forums.link }}) with a link to your pull request asking for a status update.

An instructor or teacher assistant will respond to your successful request with additional instructions. Avoid making changes to your `main` branch after requesting code review. Otherwise, you may end up with **merge conflicts** when you try to address the code review comments.

If you need to make significant changes, close the pull request, cancel your appointment, and re-request an appointment once you have a new release. Or, alternatively, make your changes in a different branch.

*If the run was not successful, the log should state why. If you are unsure how to fix the problem, reach out privately on the [course forums]({{ site.data.info.links.forums.link }}) with a link to your run asking for help.*
