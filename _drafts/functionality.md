---
title: Project Functionality
navbar: Guides
layout: guides
key: 0.3
bump: true

#tags:
#  - text: 'Updated'
#    type: 'is-info'

assignments:
  - text: 'Project 1 Functionality'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118291'
    info: '(<a href="project-1.html">Writeup</a>)'

  - text: 'Project 2 Functionality'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118292'
    info: '(<a href="project-2.html">Writeup</a>)'

  - text: 'Project 3 Functionality'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118293'
    info: '(<a href="project-3.html">Writeup</a>)'

  - text: 'Project 4 Functionality'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118294'
    info: '(<a href="project-4a.html">Writeup</a>)'
---

Each project grade is split into two components: functionality (passing tests) and design (passing code review). This guide details both the process for getting credit for project functionality. This guide assumes you have already [setup your project](setup.html) and [tested your project](testing.html). This includes making a release of your project that passes the verification process on Github.

## Eligibility

Before making a request, make sure your project is eligible to earn the functionality grade:

  - Do you have a non-zero functionality grade for the **previous** project? You can check your grades on [Canvas]({{ site.data.info.links.canvas.link }}). If you are missing a grade you should already have, please reach out to us on the [course forums]({{ site.data.info.links.forums.link }}).

      *For example, if you are on project 3, you must already have a non-zero functionality grade for project 2. If you are on project 1, you can skip this check.*

  - Are you working only **1 project ahead**?

      *For example, if you are on project 3, you must already have completed project 1 (both functionality and design) and have a non-zero functionality grade for project 2. If you are on project 1 or 2, you can skip this check.*

  - Do you have a **release for this project** that passed the verification action on Github? If not, see the [Creating Releases](testing.html#creating-releases) section of the testing guide.

If you answered yes to all of the above, you can request to have your functionality grade updated.

## Deadlines

The functionality grade is based on the **created date** of the **first passing release** on Github. This is *not* when those tests first pass locally on your system, nor the commit that first passes those tests.

There is a **2% late deduction per 24 hours** that the project functionality is late. For example, the functionality grade will be 98% if the first passing release is between 1 minute to 1 day late. The functionality grade will be 84% if the first passing release is 8 days late.

See the [Schedule](schedule.html) for the functionality deadlines.

<i class="fas fa-exclamation-triangle"></i> **New:** The late penalty will be capped at 30% maximum. If your project is significantly late, you will still be able to earn a **70%** functionality grade (assuming no other deductions).
{: .notification .is-success }

## Grading

**You only need to do this once per project.**

After verifying your project is eligible for the functionality grade, follow these steps:

  1. Browse to your private project repository on Github and click the "Actions" tab.

  2. Click on the "Request Project Grade" action on the side.

  3. Click the "Run workflow" button.

      a. Enter the project release, e.g. `v1.0.0`, that passed the tests.

      b. Enter `f`, `fun`, or `functionality` to indicate you are requesting a functionality grade.

  4. Wait for the action to finish running. When it is complete, click the "Request Project Grade" link until you see the run details.

  5. If the run was successful, **click the link to visit the issue** that was created. If everything worked properly, the issue should be assigned to a teacher assistant, have the `functionality` and `project#` labels, and belong to the `Project #` milestone (where `#` is a project number). It should also have information about your project release and expected grade.

  6. Follow the instructions on the issue. When done, **click the "Reopen issue" button**. We do not see and will not respond to un-opened issues!

  7. Wait 2 business days. If you have not heard a response by then, double check your issue is "Open" and reach out privately on the [course forums]({{ site.data.info.links.forums.link }}) with a link to your issue asking for a status update.

When the issue is closed by the instructor or teacher assistant, verify your grade was updated on Canvas.

*If the run was not successful, the log should state why. If you are unsure how to fix the problem, reach out privately on the [course forums]({{ site.data.info.links.forums.link }}) with a link to your run asking for help.*
