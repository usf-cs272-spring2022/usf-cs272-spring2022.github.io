---
title: Project 4 Web Crawler
navbar: Guides
layout: guides
key: 4.1
bump: false
project: 4

tags:
  - text: 'New'
    type: 'is-primary'

assignments:
  - text: 'Project 4 Tests'
    link: 'https://usfca.instructure.com/courses/1605147/assignments/7166809'

---

For this project, you will extend your [previous project](project-{{ page.project | minus: 1 }}.html) to create a multithreaded web crawler using a work queue that builds the inverted index from a seed URL.

**This writeup is for the web crawler functionality only.** See the general [Project 4 Final Project](project-4.html) guide for more details.

## Functionality
{: .page-header }

The core functionality of your project must satisfy the following requirements:

  - Pending


## Grading
{: .page-header }

The following sections detail how to earn credit for this project. The project grade is separated into one "functionality" or "test" grade worth 100 points, and a series of "design" or "code review" grades that together are worth another 100 points.

#### Project Tests

To be eligible for the "Project {{ page.project }} Tests" grade, you must meet the following criteria:

  - Your code must pass the tests for the current project, project {{ page.project }}.

  - Your code must pass the tests for the previous project, [project {{ page.project | minus: 1 }}](project-{{ page.project | minus: 1 }}.html).

  - You must have non-zero grades for the "Project {{ page.project | minus: 1 }} Tests" and "Project {{ page.project | minus: 1 }} Review 1" assignments in Canvas.

The tests for this project can be found in the `Project{{ page.project }}Test.java` group of JUnit tests in the [`project-tests`]({{ site.github.owner_url }}/project-tests) repository. See the [Project Testing](project-testing.html) guide for additional details.

#### Project Reviews

See the general [Project 4 Final Project](project-4.html) guide for more details on how the "design" or "review" grade for this project will be handled.

## Getting Started
{: .page-header }

The following sections may be useful for getting started on this project.

### Examples

Pending

### Related Content

The following homework assignments and lecture code may be useful to complete as part of this project:

  - Pending


### Hints

Your goal should be to get to testable code as quickly as possible first, and then to focus on passing the functionality tests. One possible breakdown of tasks are:

  - Pending

It is important to **get started early** so you have plenty of time to think about how you want to approach the project *and* start coding iteratively. Planning to complete the code in too large of a chunk is a recipe to get stuck and fall behind!

<i class="fas fa-info-circle"></i>&nbsp;These hints may or may not be useful depending on your approach. Do not be overly concerned if you do not find these hints helpful for your approach for this project.
{: .notification }


{% comment %}


## Eligibility
{: .page-header }

The eligibility requirements for this project are the same [functionality eligibility](functionality.html#eligibility) requirements of the previous projects. Specifically:

  - You must have a non-zero design grade for [project 2](project-2.html) on [Canvas]({{ site.data.info.links.canvas.link }}).

  - You must have a non-zero functionality grade for [project 3](project-3.html) on [Canvas]({{ site.data.info.links.canvas.link }}).

If you are missing a grade you should already have, please reach out to us on the [course forums]({{ site.data.info.links.forums.link }}).

## Functionality
{: .page-header }

The core functionality of your project must satisfy the following requirements:

  - Maintain the functionality of the [previous project](project-3.html).

  - Process **additional command-line parameters** to support the functionality of this project. See the [Input](#input) section for specifics.

  - Support the **same output functionality** as before. See the [Output](#output) section for specifics.

  - Add support to **build the inverted index from a seed URL** instead of a directory using a web crawler. For each page crawled, this includes:

      1. Use **sockets to download webpages** over HTTP or HTTPS, following up to 3 redirects. See the "Downloading URLs" section for details.

      2. The web crawler must **remove certain HTML block elements**, process links from the remaining HTML, and then add the found URLs to a queue for further crawling. See the "Processing URLs" for details.

      3. After processing links, **remove HTML tags and entities**, and then add the remaining stemmed words to the index. See the "Processing HTML" for details.

  - Use a work queue to **efficiently multithreaded** the web crawler such that each worker thread handles all of the processing associated with a single web page. (This includes *everything* from downloading the web page to adding the processed text to the inverted index.)

  - To avoid a infinite crawl, the web crawler should crawl up to a **fixed limit of unique URLs** (including the seed URL).

  - Your code may *NOT* use any of the classes in the `java.util.concurrent` package.

The functionality of your project will be evaluated with various JUnit tests. Please see the [Testing](#testing) section for specifics.

### Downloading URLs

For each unique normalized URL that must be crawled (up until the limit), the worker thread must:

  - Use sockets, NOT use the URL class, to download the web page over HTTP or HTTPs.

  - If the HTTP response status was a redirect, follow the redirect up to a limit of 3 redirects (to avoid an infinite redirect loop). The content at the end of this process will be assigned to the original URL.

    For example, the URL [~cs212/redirect/one](https://www.cs.usfca.edu/~cs212/redirect/one) eventually redirects to [~cs212/simple/hello.html](https://www.cs.usfca.edu/~cs212/simple/hello.html). However, the web crawler will associate the content of [~cs212/simple/hello.html](https://www.cs.usfca.edu/~cs212/simple/hello.html) with the original link [~cs212/redirect/one](https://www.cs.usfca.edu/~cs212/redirect/one) instead.

  - If the HTTP response status code is `200 OK` and the content-type is HTML, download the HTML (without other HTTP headers) for additional processing.

See the next section for how to process the downloaded HTML content.

### Processing URLs

Once the HTML has been downloaded, the next step is to process that HTML to find additional links to crawl. Specifically:

  - Remove any HTML comments and block elements that should not be considered for parsing links, including the `head`, `style`, `script`, `noscript`, and `svg` elements.

  - Parse all of the URLs remaining on the page, and convert them to normalized absolute form (remove fragments, convert relative URLs to absolute URLs, etc.).

  - For each of the processed absolute URLs, queue a new crawl of that URL if:

    1. The maximum crawl limit has not yet been reached.

    2. This URL has not already been crawled or queued to be crawled.

If using the work queue properly and the maximum limit is 50 URLs, then the first 49 unique URLs on the seed page (plus the seed URL itself) will be part of the crawl.

### Process HTML

Once the links have been processed, the next step is to process the remaining HTML and add the stemmed content to the index. Specifically:

  - Remove all of the remaining HTML tags.

  - Convert any HTML 4 entities to their Unicode symbol and remove any other HTML entities found that could not be converted.

  - Clean, parse, and stem the resulting text.

  - Efficiently add the stems to the inverted index.

## Input
{: .page-header }

Your main method must be placed in a class named `Driver`. The `Driver` class should accept the following **additional** command-line arguments:

  - `-html seed` where `-html` indicates the next argument `seed` is the seed URL your web crawler should initially crawl to build the inverted index.

      If the `-html` flag is provided, your code should **enable multithreading** with the default number of worker threads even if the `-threads` flag is not provided.

  - `-max total` where `-max` is an *optional* flag that indicates the next argument `total` is the total number of URLs to crawl (including the seed URL) when building the index. Use `1` as the default limit if this flag is not provided or is not provided with a valid value.

The command-line flag/value pairs may be provided in any order, and the order provided is not the same as the order you should perform the operations (i.e. always build the index before performing search, even if the flags are provided in the other order).

Your code should support all of the command-line arguments from the [previous project](project-3.html) as well.

## Output
{: .page-header }

The output of your inverted index and search results should be the same from the [previous project](project-3.html). As before, you should **only generate output files if the necessary flags are provided**.

## Testing
{: .page-header }

You must pass 100% of the tests in the `Project4Test.java` group of JUnit tests. This test group does NOT include the long-running runtime tests that benchmark your single- versus multi-threading code for the [previous project](project-3.html). However, it does make sure your new web crawler code runs faster with 3 threads versus 1 thread.

<article class="message is-info">
  <div class="message-body">
    <i class="fas fa-info-circle"></i>&nbsp;These tests are only for the web crawler functionality. The search engine functionality will be verified during the final code review appointment, not via automated system tests.
  </div>
</article>

## Related Content
{: .page-header }

The following content from this semester may be helpful in completing this project:

  - The `LoggerSetup` homework assignment demonstrates how to configure `log4j2` to debug code.

  - The `Sockets` lecture code illustrates how to use sockets and create HTTP requests (useful for the `HtmlFetcher` homework).

  - The `HtmlFetcher` homework assignment will help follow HTTP redirects and download HTML over a socket connection. <i class="fas fa-star has-text-usf-gold"></i>

  - The `HtmlCleaner` homework assignment will help process the download HTML. Be careful about how much HTML content is removed before links are parsed! <i class="fas fa-star has-text-usf-gold"></i>

  - The `LinkParser` homework assignment will help parse links from HTML (after block elements are removed). <i class="fas fa-star has-text-usf-gold"></i>

  - The `TextFileStemmer` homework assignment will help parse the remaining content after cleaning the HTML into stems to add to the inverted index.

  - The `WorkQueues` lecture code illustrates how to use a work queue and create tasks for recursive problems (like web crawling). <i class="fas fa-star has-text-usf-gold"></i>

  - The `WorkQueues` lecture code illustrates how to speed up multithreading code and avoid problems with over-blocking.

It is strongly recommended to pass all of the homework tests before integrating them into your projects.

## Hints
{: .page-header }

It is important to develop the project iteratively. One possible breakdown of tasks are:

  - Get `log4j2` working and start adding debug messages in your code. Once you are certain a class is working, disable debug messages for that class in your `log4j2.xml` file.

  - You must have an efficient approach to multithreading to pass all of the tests. You should wait until you have at least one project 3 code review and are able to pass those runtime tests before starting this project.

  - Outside of the relevant homework and lecture classes, there is likely only one new class (a web crawler class) required for this project. However, you must be careful to properly multithread and synchronize in this class!

The important part will be to test your code as you go. The JUnit tests provided only test the entire project as a whole, not the individual parts. You are responsible for testing the individual parts themselves.
{% endcomment %}
