---
title: Project 4 Search Engine
navbar: Guides
layout: guides
key: 4.2
bump: false
project: 4

tags:
#  - text: 'Pending'
#    type: 'is-muted'
  - text: 'New'
    type: 'is-primary'

assignments:
  - text: 'Project 4 Search Engine'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118300'
---

For this project, you will extend your [previous project](project-4a.html) to create a search engine web interface using embedded Jetty and servlets.

**This writeup is for the search engine functionality only.** See the general [Project 4 Writeup](project-4.html) for more details.

## Eligibility
{: .page-header }

To be eligible for the "Project 4 Search Engine" grade, you must meet the following criteria:

  - You must have a non-zero grade for the "Project {{ page.project | minus: 1 }} Final Release" assignment in Canvas.

  - You must have a non-zero grade for the "Project {{ page.project }} Tests" assignment in Canvas and your code must still pass the associated tests.

  - Your code must additionally pass the code review checks, and you must attend a code review with the instructor.

See the [final code review](final-review.html) guide for the deadline to meet the eligibility requirements to qualify for this project assignment.

## Functionality
{: .page-header }


The functionality for this project is broken into 2 parts: core functionality and extra features. **You must complete the core functionality before attempting extra functionality.**

### Core Functionality

In addition to maintaining the functionality of the [previous project](project-4a.html), your code must support the following core features using embedded Jetty and servlets for a total of 30 points:

| Points | Functionality Description |
|:------:|:--------------------------|
| 5 | **Web Form:** Display a web page with a form that includes (at a minimum) a text box where users may enter a multi-word search query and a button to submit that query to the web server. |
| 5 | **Query Processing:** When the web form button is clicked, send the queries to a Jetty servlet and process those queries to match how the data is stored by your inverted index. |
| 10 | **Partial Search:** After processing the queries, the servlet should retrieve the partial search results of those queries from the index generated by the `Driver` class. |
| 10 | **Search Results:** The servlet should return the partial search results to the client (or web browser) as dynamically generated HTML with sorted (most relevant first) and clickable links. |
{: .table .is-hoverable }

You cannot earn credit for additional features until the core functionality is working properly.

### Additional Functionality

Once the core functionality is complete, you may implement 70 points of additional features. These features are broken into several categories. You may choose any combination of features from these categories.

Have a feature idea? You can propose an extra feature in a public post on the course forums. If approved, the instructor will post the number of points that feature will be worth on the final project.
{: .notification .is-info .is-light }

#### User Tracking

The following features requires your search engine to track user data. There are two implementation options (choose one):

  1. **Base Functionality:** Implemented by storing data in memory; only supports a single user.

  2. **Extra Functionality:** Implemented by storing data using session tracking or cookies; supports multiple users.

Ideally, you should use the same implementation option for all features in this subcategory. For example, if you implement search history using sessions, you should also implement visited results using sessions.

The possible features are:

| Base | Extra | Functionality Description |
|:----:|:-----:|:--------------------------|
| 5 | 10 | **Search History:** Store a history of all search queries. Allow users to view and clear that history. |
| 5 | 10 | **Visited Results:** Store a history of all visited search results (i.e. results clicked on). Allow users to view and clear that history. |
| 5 | 10 | **Favorite Results:** Allow users to save favorite search results. Allow users to view and clear those favorites. |
| 5 | 5 | **Time Stamps:** Add timestamps to each item stored. Implement this for all related features to earn full credit. |
| 5 | 5 | **Private Search:** Allow users to set an option that turns off all tracking of user data. Implement this for all related features to earn full credit. |
| 5 | 5 | **Last Visit Time:** Track and display the last time a user visited your search engine. This is NOT the current time that the page was generated! |
{: .table .is-hoverable }

There are 30 to 45 points possible in this category depending if you choose to implement base or extra functionality.

#### Metadata

The following features requires your search engine to track search metadata (not specific to users). There are two implementation options:

  1. **Base Functionality:** Track metadata in memory (non-persistent).

  2. **Extra Functionality:** Track metadata in the on-campus SQL database (persistent).

Ideally, you should use the same implementation option for all features in this subcategory. For example, if you implement page snippets using a database, you should also implement popular queries using a database too.

The possible features are:

| Base | Extra | Functionality Description |
|:----:|:-----:|:--------------------------|
| 10 | 20 | **Page Snippets:** When a web page is crawled, store a short snippets of the page. Display the snippet whenever that page is returned as a result. |
| 10 | 20 | **Page Statistics:** When a web page is crawled, store the page title (via the `<title>` tag in HTML), content length (via the `Content-Length` HTTP header), and timestamp of the crawl. Display these statistics whenever that page is returned as a result. |
| 5 | 10 | **Most Visited Results:** Track the number of times a page has been visited by any user. Allow users to see the top 5 visited pages. |
| 5 | 10 | **Most Searched Queries:** Track the number of times a multi-word query has been searched for. Allow users to see the top 5 most popular queries. |
| 5 | 10 | **Reset Metadata:** Allow users with an administrator password to clear all the metadata stored. |
{: .table .is-hoverable }

Some features require others to be implemented first. For example, **Reset Metadata** cannot be implemented until at least one of the other features that stores metadata is implemented.

There are 35 to 70 points possible in this category depending if you choose to implement base or extra functionality.

#### Extendable Functionality

The following features have base functionality that can be extended with additional functionality. The base functionality must be implemented first.

| Base | Extra | Base Functionality | Extended Functionality |
|:----:|:-----:|:-------------------|:-----------------------|
| 5 | 10 | **New Seed:** Allow a user to specify a new seed URL that should be added to the existing inverted index. If the URL has already been crawled, skip crawling that URL and output a warning to the user. | **Max Support:** In addition to entering a new seed URL, allow the user to also specify a maximum number of pages to crawl. This is the maximum number of new pages to crawl in addition to the pages already crawled. URLs that are already included in the inverted index should be skipped and should not contribute to this maximum count. |
| 5 | 10 | **Index Browser:** Allow users to browse your inverted index as an HTML page with all of the words stored, clickable links to all of the indexed URLs for those words, and the number of positions stored for that word and location (but not list all of the positions). | **Subindex Browser:** Allow users to enter a specific word and display the data stored in your inverted index for that specific word. |
| 5 | 10 | **Location Browser:** Allow users to browse all of the locations and their word counts stored by your inverted index as an HTML page with clickable links to all of the indexed URLs. | **Partial Location Search:** Allow users to browse all of the locations and their word counts for locations that start with the same text. For example, browse all locations that start with ???http://www.cs.usfca.edu/~cs272???. |
{: .table .is-hoverable }

For example, if you implement base functionality for **New Seed**, you will earn 5 points. If you implement both base and extra functionality for **New Seed** (including **Max Support**), you will earn 10 points instead.

There are 15 to 30 points possible in this category depending if you choose to implement base or extra functionality.

#### Miscellaneous Functionality

The following miscellaneous features may also be implemented:

| Points | Functionality Description |
|:------:|:--------------------------|
| 5 | **Graceful Shutdown:** Allow an administrator to trigger a graceful shutdown of your search engine without calling `System.exit()``. |
| 5 | **Search Statistics:** Display the total number of results along with the time it took to calculate and fetch those results, and display the score and number of matches per search result listed. |
| 5 | **Server Statistics:** As a footer on every page, display the server uptime (i.e. time since the server was started), total number of words stored, total number of locations stored, and total number of queries conducted. This information can be stored in memory by the server. |
| 5 | **Quick Search:** Add a new button to your search form (in addition to the normal search button) that automatically redirects the user to the first search result instead of listing all of the search results. This is similar to the Google Search "I'm Feeling Lucky" button. Output a warning if there are no search results. |
| 5 | **Reverse Sort Order:** Allow the user to select an option to reverse the sort order of the search results using a checkbox on the search form. |
| 5 | **Partial/Exact Search Toggle:** Allow the user to toggle on/off partial versus exact search using a checkbox on the search form. |
| 5 | **Web Framework:** Design a search engine using any popular CSS/style framework to create a consistent style for all the web pages. For example, consider using [Bulma](https://bulma.io/), [Bootstrap (Twitter)](https://getbootstrap.com/), [Pure.css](https://purecss.io/), [Material (Google)](https://material.io/develop/web/), [Semantic UI](https://semantic-ui.com/), and many more. |
| 5 | **Search Brand:** Design a search engine with a distinct brand, logo, and tagline. This includes creating a logo and tagline, and including it on all of the web pages. **Do not use unlicensed unattributed media on your website.**{: .has-text-danger }  |
| 5 | **Light/Dark Mode Toggle:** Allow users to toggle between light mode (light colored background with dark text) and dark mode (dark colored background with light text) styles for your website. |
{: .table .is-hoverable }

There are 45 points possible in this category.

### Input

Your main method must be placed in a class named `Driver`. The `Driver` class should accept the following **additional** command-line arguments:

  - `-server [port]` where the flag `-server` indicates to launch a search engine web server, and the next *optional* argument `[port]` is the port the web server should use to accept socket connections. Use `8080` as the default value if it is not provided.

    If the `-server` flag is provided, your code should **enable multithreading** with the default number of worker threads even if the `-threads` flag is not provided.

The command-line flag/value pairs may be provided in any order, and the order provided is not the same as the order you should perform the operations (i.e. always build the index before performing search, even if the flags are provided in the other order).

Your code should support all of the command-line arguments from the [previous project](project-4a.html) as well.

### Output

The output of your inverted index and search results should be the same from the [previous project](project-4a.html). As before, you should **only generate output files if the necessary flags are provided**.

## Grading
{: .page-header }

The following sections detail how to earn credit for this project.

#### Project Tests

There are no tests specifically for the **Project 4b Search Engine** other than the [Project 4a Web Crawler](project-4a.html) tests provided.

#### Project Reviews

The search engine functionality will be demonstrated in a single code review during finals week (if eligible). See the general [Final Code Review](final-review.html) guide for more details on how this last code review will be handled.

#### Potential Deductions

It is possible to lose points earned for additional functionality if your implementations have any of the following issues:

| Points | Deduction Description |
|:------:|:----------------------|
| -10 | **Multi-User Support:** Deducted if your code does not support multi-user search. Users conducting search simultaneously should see results relevant to their own queries only. |
|  -5 | **Thread Saftey:** Deducted if your code is not thread-safe. In-memory data accessed by different threads should be properly protected. |
|  -5 | **Cross-Site Scripting (XSS) Vulnerabilities:** Deducted if your code does not protect against cross-site scripting (XSS) attacks. Escape or sanitize any data from a user (either via the HTTP request or a database) prior to using it on an HTML page. |
|  -5 | **SQL Injection Vulnerabilities:** Deducted if your code does not protect against SQL injection attacks. Use prepared statements where appropriate anytime it accesses a database. |
|  -5 | **Poor Encapsulation:** Deducted if your code breaks encapsulation. |
|  -5 | **Poor Code Style:** Deducted if your code is not professional. Use professional formatting, variable names, Javadoc, exception handling, and address all compiler warnings. |
{: .table .is-hoverable }

These deductions will only come out of the points earned for additional functionality---they will not impact points earned for core functionality.

While there are many ways to lose points, the total possible deduction is capped such that no more than 20 points total will be removed from your project grade due to the above issues.

#### Extra Credit

You may complete additional functionality as extra credit. You can earn up to 120% on this project assignment.

Regardless of what you implemented, you will NOT earn points for the search engine core functionality if you are not passing all of the web crawler tests, and will NOT earn points for extra functionality if you have not fully implemented the core functionality!
{: .notification .is-warning .is-light }

## Getting Started
{: .page-header }

The following sections may be useful for getting started on this project.

### Examples

The following are a few examples (non-comprehensive) to illustrate the usage of the command-line arguments that can be passed to your `Driver` class via a "Run Configuration" in Eclipse, assuming you set the working directory to the `project-tests` directory.

Consider the following example:

```
-html "https://usf-cs272-spring2022.github.io/project-web/input/simple/" -max 15 -threads 3 -server 8080
```

The above arguments behave the same as [project {{ page.project | minus: 1 }}](project-{{ page.project | minus: 1 }}.html), except it will also start up a web server on port `8080` for the user to interface with the search engine. No file output will be generated in this example.

### Related Content

The following homework assignments and lecture code may be useful to complete as part of this project:

  - The `ServletBasics` and `ServletData` lecture code illustrates how to use embedded Jetty and servlets to create a basic web interface. The `ReverseServer` example is most relevant for basic search functionality.

  - The `HeaderServer` homework assignment illustrates how to use web forms with embedded Jetty and servlets.

  - The `Sessions` lecture code illustrates how to enable user tracking (optional).

  - `JDBC` lecture code illustrates how to connect servlets to a SQL database on campus (optional).

You can modify homework assignments and lecture code as necessary for this project. However, for homework, make sure your code is passing all of the tests before using.

You should *not* wait until you have completed all of the associated homework assignments or covered all of the related lecture content to start the project. You should **develop the project iteratively** as you progress throughout the semester, integrating assignments and concepts one at a time into your project code.

### Hints

Your goal should be to get to testable code as quickly as possible first, and then to develop the project iteratively. Some considerations to make while developing are:

  - Start with using `GET` requests for basic search functionality.

  - Using `POST` requests are usually only useful for user tracking features, and it is possible to implement those features using only `GET` as well.

  - To ensure multi-user support, avoid static and instance members for storing anything related to search queries and results in your servlets.

  - For visited and favorite results, modify the search result links to direct back to your search engine, so that it may first store that the link was clicked on and then redirect as necessary.

  - For crawl metadata, modify the web crawler to store more information per crawl (instead of just which unique URLs have been crawled).

  - For graceful shutdown, you will need to create a special servlet combined with the [ShutdownHandler](https://www.eclipse.org/jetty/javadoc/jetty-11/org/eclipse/jetty/server/handler/ShutdownHandler.html) in Jetty.

The important part will be to test your code as you go. Use the JUnit tests provided for previous projects to come up with your own test cases.
