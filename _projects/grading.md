---
title: Project Grading
navbar: Guides
layout: guides
key: 0.3

#tags:
#  - text: 'Updated'
#    type: 'is-info'

tags:
  - text: 'New'
    type: 'is-primary'

assignments:
  - text: 'Project 1 Inverted Index'
    link: 'project-1.html'

  - text: 'Project 2 Partial Search'
    link: 'project-2.html'

  - text: 'Project 3 Multithreading'
    link: 'project-3.html'

  - text: 'Project 4 Search Engine'
    link: 'project-4.html'
---

Each project grade is split into multiple assignments to evaluate the functionality (passing tests) and design (passing code review) of your projects. This guide details the process for getting credit for these project assignments.


This guide assumes you have already [setup your project](setup.html) and [tested your project](testing.html). This includes making a release of your project that passes the checks on GitHub.
{: .notification }

## Requesting Project Grades
{: .page-header }

All grade and code review requests start the same way: opening an [**Issue**](https://docs.github.com/en/issues) on GitHub. Your project template already comes with four possible issue types:

![Screenshot]({{ "/images/github-issue-templates.png" | relative_url }}){: style="width: 400px;" class="is-size is-bordered" }

After choosing the appropriate issue template, you will see instructions to:

  1. Replace `v0.0.0` in the issue title with the release you want graded.
  2. Replace `FULL_NAME` with your first and last name in the issue body.
  3. Replace `USF_USERNAME` with your USF username (*not* your Github username) in the issue body.

See [this issue](https://github.com/usf-cs272-spring2022/project-template/issues/1) for an example of what the title and body should look like.

After opening the issue, you should see the message:

> 🤖 The GitHub Actions bot is now processing your request...

You can visit the linked action run to see the bot progress. Eventually, the bot will respond again with whether your request succeeded or failed. If the request fails, the bot will apply the `error` tag and close the issue.

**Closed issues or issues with the `error` tag will not be processed by the instructor or teacher assistants.** You will have to fix the issue, manually remove the `error` tag, and then re-open the issue to re-trigger the GitHub Actions bot to check your request again.

The next sections cover more specifics about each different type of request.

## Request Project Tests Grade
{: .page-header }

There is only one assignment associated with project functionality: the `Project # Tests` assignment, where `#` is either the `1`, `2`, `3`, or `4` project number. This assignment requires you pass the appropriate tests when run by GitHub Actions. See below for details.

### Eligibility

Before requesting the "Project # Tests" assignment grade, you need a release that passed the functionality tests. The release description added by GitHub Actions must have the "Project Test" checkmark selected. For example:

> #### Eligibility
>
> - [x] &nbsp;Project Test
> - [ ] &nbsp;Project Review
>
> #### Status
>
> 🔔 The release `v1.0.1` passed all project 1 tests, but did not pass one or more of the other checks required for code review. This release may be used to request a project test grade only. See [run id 1234567890](#) for details.
{: style="background-color: white;" }

You can also verify this by visiting the GitHub Actions run and checking that the "Check / Release Number" and "Check / JUnit Tests" jobs have a green circle <i class="fas fa-check-circle has-text-success"></i> icon indicating they succeeded. These jobs will make sure that:

  1. The release is properly created using the `v#.#.#` format where the first `#` is the project being tested and the second `#` is the number of code reviews already conducted for that project.

  1. The release is for a project you are eligible to earn the `Project # Tests` grade. **You may only work ahead by one project.** Specifically, for projects 2, 3, and 4, you must already have a `Project # Tests` and `Project # Review 1 ` grade for the previous project.

  1. The JUnit tests for the *current* project functionality pass. This includes all tests with the `test#` tag pass, where `#` is the current project being tested.

  2. The JUnit tests for the *previous* projects functionality (for projects 2, 3, and 4) still pass. This includes all tests with the `past#` tag.

  3. The JUnit tests that make sure the *next* project functionality is not yet implemented pass. This includes all tests with the `next#` tag. **You cannot implement the next project functionality in the same branch as the current project.**

If the release indicated by the issue title meets these requirements, the GitHub Actions bot will calculate your grade.

### Grading

The `Project # Tests` assignment is worth `100` points total. You will earn the maximum score if you create a release that passes the functionality tests on GitHub actions before the deadline posted on the course schedule. Otherwise, you will lose `2` points per `1` day your project functionality is late up to a maximum penalty of `26` points.

For example, if the deadline is March 1 at 11:59pm and the project release that first passes the tests on GitHub was created on March 2 at 12:05am, the late penalty will be `2 * 1 = 2` and you will earn `100 - 2 = 98` points on the assignment. If your release is `14` days late, the late penalty will be `26` since `2 * 14 = 28` is greater than the maximum penalty of `26`. The resulting grade in that case will be `74` points.

## Request Code Review Appointment
{: .page-header }

After passing functionality, the design of your project is evaluated via 2 or more code review appointments. The design grade is broken up into multiple assignments to track your process:

  - **Project # Review 1**: Earned after attending your first code review for the `#` project.
  - **Project # Review 2**: Earned after attending your second code review for the `#` project.
  - **Project # Final Release**: Earned after passing code review and creating a final release of the `#` project.

You must request and attend a code review appointment to be eligible for these grades. See below for details.

The code review process for project 4 is handled differently, since it occurs during finals week at the end of the semester. Additional details for the last code review will be posted towards the end of the semester.
{: .notification }

### Eligibility

Before requesting a code review appointment, you need a release that passed the functionality tests *and* style checks. The release description added by GitHub Actions must have the "Project Test" and "Project Review" checkmarks selected. For example:

> #### Eligibility
>
> - [x] &nbsp;Project Test
> - [x] &nbsp;Project Review
>
> #### Status
>
> 💯 The release `v1.0.2` passed all project 1 tests and checks. This release may be used to request a project test grade or request code review. See [run id 1234567890](#) for details.
{: style="background-color: white;" }

You can also verify this by visiting the GitHub Actions run and checking that the following jobs have a green circle <i class="fas fa-check-circle has-text-success"></i> icon indicating it succeeded:

  1. The "Check / Code Warnings" job, which checks that `javac` compiles the code without any warnings.

  2. The "Check / Javadoc Warnings" job, which checks that `javadoc` compiles the Javadoc comments without any warnings.

  3. The "Check / Code Style" job, which checks for basic cleanup tasks (like removing `TODO` comments, extra `main` methods, and stack traces).

If the release indicated by the issue title meets these requirements, the GitHub Actions bot will setup a pull request and give you instructions for how to sign up for an appointment. Keep in mind that you may only have up to 1 code review appointment with the instructor every 5 days.

### Grading

You receive grades for your first two code review appointments, and for the final release of your project created after you pass code review. Additional code reviews after the first two are not graded or penalized. See the following sections for details.

Make sure to attend your appointment on-time. You will receive one warning if you arrive more than 5 minutes late or miss an appointment. After a warning, you may choose one of two penalties: lose **5** points per additional late or missed appointment or wait another **5** days for your next appointment.
{: .notification .is-danger }

## Request Project Review Grade
{: .page-header }

TL;DR You must attend your code review on-time. For the first code review, this is by the deadline listed on the course schedule. For the second code review, this is within 10 days of the first code review.

### Eligibility

Pending

### Grading

Pending

## Request Project Final Release Grade
{: .page-header }

TL;DR You must pass code review and create a final release that passes all of the checks within 10 days of the last code review.

### Eligibility

Pending

### Grading

Pending
