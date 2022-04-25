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

  - Maintain the functionality of the [previous project](project-{{ page.project | minus: 1 }}.html).

  - Process **additional** command-line arguments to determine the input to process and output to produce. See the "Input" and "Output" sections below for specifics.

  - Add support to **build the inverted index from a seed URL** instead of a directory using a web crawler. For each page crawled, this includes:

      1. Use **sockets to download webpages** over HTTP or HTTPS, following up to 3 redirects. See the "Downloading URLs" section for details.

      2. The web crawler must **remove certain HTML block elements**, process links from the remaining HTML, and then add the found URLs to a queue for further crawling. See the "Processing URLs" for details.

      3. After processing links, **remove HTML tags and entities**, and then add the remaining stemmed words to the index. See the "Processing HTML" for details.

  - When crawling, **download the content only once** from the web server and only if necessary.

      - Do not fetch the web page content more than once. For example, do not fetch the entire web page content once to check the headers and again to process the HTML.

      - Do not fetch the web page content if it is not HTML. For example, for large text file without the `text/html` content-type, there is no need to download any of the content that appears after the headers.

      - Do not fetch the web page if it has already been encountered before, regardless of whether it was added to the index or skipped (due to an invalid type or status code).

  - Use a work queue to **efficiently multithreaded** the web crawler such that each worker thread handles all of the processing associated with a single web page. This includes *everything* from downloading the web page to adding the processed text to the inverted index.

  - To avoid a infinite crawl, the web crawler should crawl up to a **fixed limit of unique URLs** (including the seed URL).

  - Do *NOT* use any of the classes in the `java.util.concurrent` package and do *NOT* use the `Stream.parallel` method for the multithreaded code.

See the following sections for additional details.

### Downloading URLs

For each unique normalized URL that must be crawled (up until the limit), the worker thread must:

  - Use sockets, NOT use the URL class, to download the web page over HTTP or HTTPs.

  - If the HTTP response status was a redirect, follow the redirect up to a limit of 3 redirects (to avoid an infinite redirect loop). The content at the end of this process will be assigned to the original URL.

    For example, the URL [~cs212/redirect/one](https://www.cs.usfca.edu/~cs212/redirect/one) eventually redirects to [~cs212/simple/hello.html](https://www.cs.usfca.edu/~cs212/simple/hello.html). However, the web crawler will associate the content of [~cs212/simple/hello.html](https://www.cs.usfca.edu/~cs212/simple/hello.html) with the original link [~cs212/redirect/one](https://www.cs.usfca.edu/~cs212/redirect/one) instead.

  - If the HTTP response status code is `200 OK` and the content-type is `text/html`, download the HTML (without other HTTP headers) for additional processing.

See the next section for how to process the downloaded HTML content.

### Processing URLs

After the HTML has been downloaded, the next step is to process that HTML to find additional links to crawl. Specifically:

  - Remove any HTML comments and block elements that should not be considered for parsing links, including the `head`, `style`, `script`, `noscript`, and `svg` elements.

  - Parse all of the URLs remaining on the page, and convert them to normalized absolute form (e.g. remove fragments, convert relative URLs to absolute URLs).

  - For each of the processed absolute URLs, queue a new crawl of that URL if:

    1. The maximum crawl limit has not yet been reached.

    2. This URL has not already been crawled or queued to be crawled.

If using the work queue properly and the maximum limit is 50 URLs, then the first 49 unique URLs on the seed page (plus the seed URL itself) will be part of the crawl.

### Process HTML

After the links have been processed, the next step is to remove the remaining HTML markup. The remaining text must be cleaned and stemmed the same way as text files. Specifically:

  - Remove all of the remaining HTML tags.

  - Convert any HTML 4 entities to their Unicode symbol and remove any other HTML entities found that could not be converted.

  - Clean, parse, and stem the resulting text.

  - Efficiently add the stems to the inverted index.

Once the stems are added to the index, the search functionality should work the same as before.

### Input

Your `main` method must be placed in a class named `Driver`. The `Driver` class should accept the following additional command-line arguments:

  - `-html [seed]` where the flag `-html` indicates the next argument `[seed]` is the seed URL your web crawler should initially crawl to build the inverted index. If the `-html` flag is provided, your code should **enable multithreading** with the default number of worker threads even if the `-threads` flag is not provided.

  - `-max [total]` where the flag `-max` is an *optional* flag that indicates the next argument `[total]` is the total number of URLs to crawl (including the seed URL) when building the index. If the `[total]` argument is not provided or an invalid number, use `1` as the default value.

The command-line flag/value pairs may be provided in any order, and the order provided is not the same as the order the code should perform the operations (i.e. always build the index before performing search, even if the flags are provided in the other order).

Your code should support all of the command-line arguments from the [previous project](project-{{ page.project | minus: 1 }}.html) as well.

### Output

The output of your inverted index and search results should be the same from the [previous project](project-{{ page.project | minus: 1 }}.html).

As before, your code should **only generate output files if the necessary flags are provided**. If the correct flags are provided, your code should perform the indexing and search operations even if file output is not being generated.

## Grading
{: .page-header }

The following sections detail how to earn credit for this project. The project grade is separated into one "functionality" or "test" grade worth 100 points, and a series of "design" or "code review" grades that together are worth another 100 points.

#### Project Tests

To be eligible for the "Project {{ page.project }} Tests" grade, you must meet the following criteria:

  - Your code must pass the tests for the current project, project {{ page.project }}.

  - Your code must pass the tests for the previous project, [project {{ page.project | minus: 1 }}](project-{{ page.project | minus: 1 }}.html).

  - You must have non-zero grades for the "Project {{ page.project | minus: 1 }} Tests" and "Project {{ page.project | minus: 1 }} Review 1" assignments in Canvas.

The tests for this project can be found in the `Project{{ page.project }}Test.java` group of JUnit tests in the [`project-tests`]({{ site.github.owner_url }}/project-tests) repository. See the [Project Testing](project-testing.html) guide for additional details.

<article class="message is-warning">
  <div class="message-body"><i class="far fa-exclamation-triangle"></i>&nbsp;Run only the exact tests needed for debugging! Running all of the tests too often could result in getting blocked or rate-limited by the web server or your network provider!</div>
</article>

#### Project Reviews

See the general [Project 4 Final Project](project-4.html) guide for more details on how the "design" or "review" grade for this project will be handled.

## Getting Started
{: .page-header }

The following sections may be useful for getting started on this project.

### Examples

The following are a few examples (non-comprehensive) to illustrate the usage of the command-line arguments that can be passed to your `Driver` class via a "Run Configuration" in Eclipse, assuming you set the working directory to the `project-tests` directory.

Consider the following example:

```
-html "https://usf-cs272-spring2022.github.io/project-web/input/simple/" -limit 15 -threads 3 -index index-crawl.json
```

The above arguments behave the same as [project {{ page.project | minus: 1 }}](project-{{ page.project | minus: 1 }}.html), except it will build the index from a seed web page and process up to `15` found links from that seed page.

```
-html "https://usf-cs272-spring2022.github.io/project-web/input/simple/" -index index-crawl.json
```

The above arguments are nearly the same, except use the default of `1` for the limit and `5` worker threads.

### Related Content

The following homework assignments and lecture code may be useful to complete as part of this project:

  - The `LoggerSetup` homework is useful for learning how to set up and configure `log4j2`, which will be helpful when it comes to debugging multithreaded code.

  - The `Sockets` lecture code illustrates how to use sockets and create HTTP requests (useful for the `HtmlFetcher` homework).

  - The `HtmlFetcher` homework is useful for following HTTP redirects and downloading HTML over a socket connection. This homework can be used directly for your project.

  - The `HtmlCleaner` homework is useful for processing the download HTML. This homework can be used directly for your project, but be careful about how much HTML content is removed before links are parsed!

  - The `LinkParser` homework is useful for parsing links from HTML (after block elements are removed). This homework can be used directly for your project.

  - The `TextFileStemmer` homework is useful for converting cleaned HTML into word stems. This homework can be used directly for your project.

  - The `WorkQueues` lecture code illustrates how to use a work queue and create tasks for recursive problems (like web crawling).

You can modify homework assignments and lecture code as necessary for this project. However, for homework, make sure your code is passing all of the tests before using.

You should *not* wait until you have completed all of the associated homework assignments or covered all of the related lecture content to start the project. You should **develop the project iteratively** as you progress throughout the semester, integrating assignments and concepts one at a time into your project code.

### Hints

Your goal should be to get to testable code as quickly as possible first, and then to focus on passing the functionality tests. One possible breakdown of tasks are:

  - Configure `log4j2` add debug messages in your code. Once you are certain a class is working, disable debug messages for that class in your `log4j2.xml` file.

  - Your code must have an efficient approach to multithreading to pass the runtime tests. Wait until you are able to pass the runtime tests of the previous project before worrying about efficiency for this project.

  - Outside of the relevant homework and lecture classes, there is likely only one new class (a web crawler class) required for this project.

It is important to **get started early** so you have plenty of time to think about how you want to approach the project *and* start coding iteratively. Planning to complete the code in too large of a chunk is a recipe to get stuck and fall behind!

<i class="fas fa-info-circle"></i>&nbsp;These hints may or may not be useful depending on your approach. Do not be overly concerned if you do not find these hints helpful for your approach for this project.
{: .notification }
