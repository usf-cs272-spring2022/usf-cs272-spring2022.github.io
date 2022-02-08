---
title: Project 2 Partial Search
navbar: Guides
layout: guides
key: 2.0
bump: false
project: 2

tags:
  - text: 'Pending'
    type: 'is-muted'

assignments:
  - text: 'Project 2 Tests'
    link: 'https://usfca.instructure.com/courses/1605147/assignments/7166801'

  - text: 'Project 2 Review 1'
    link: 'https://usfca.instructure.com/courses/1605147/assignments/7166802'

  - text: 'Project 2 Review 2'
    link: 'https://usfca.instructure.com/courses/1605147/assignments/7166803'

  - text: 'Project 2 Final Release'
    link: 'https://usfca.instructure.com/courses/1605147/assignments/7166804'

---

Pending

{% comment %}
TO ADD:

To be eligible for the "Project 2 Tests" grade, you must meet the following criteria:

  - You must have a non-zero grade for the "Project 1 Tests" and "Project 1 Review 1" assignments in Canvas.

  - Your code must pass the tests for the previous project, project 1.

  - Your code must pass the tests for the current project, project 2.

  - Your code must *not* pass the tests for the future project, project 3.

See the [Project Testing](project-testing.html) guide for additional details.


For this project, you will extend your [previous project](project-1.html) to support exact search and partial search. In addition to meeting the [previous project](project-1.html) requirements, your code must be able to track the total number of words found in each text file, parse and stem a query file, generate a sorted list of search results from the inverted index, and support writing those results to a JSON file.

## Functionality
{: .page-header }

The core functionality of your project must satisfy the following requirements:

  - Maintain the functionality of the [previous project](project-1.html).

  - Process **additional command-line parameters** to determine whether to search the inverted index and whether to produce additional JSON ouput. See the "Input" section for specifics.

  - Modify how input text files are processed to also **track the total word count of each file** when storing it in the inverted index. See the "Word Count" section for specifics.

  - Parse a query file line-by-line into a **normalized and optimized multiple-word queries matching** the processing used to build the inverted index. See the "Query Parsing" section for specifics.

  - Efficiently return **exact search results** from your inverted index, such that results from any word stem in your inverted index that exactly matches a query word is returned.

  - Efficiently return **partial search results** from your inverted index, such that results from any word stem in your inverted index that starts with a query word is returned.

  - Sort the search results using a simple **term frequency metric** to determine the most "useful" search results to output first. See the "Result Sorting" section for specifics.

The functionality of your project will be evaluated with the `Project2Test.java` group of JUnit tests. See the "Testing" section for details.

### Word Count

Before you can calculate search results, you need to know how many word stems were stored in your inverted index for each text file.

**Avoid opening up any file more than once!** You should store this information alongside the inverted index, as the files are first processed.

These word counts will be output to file using the same pretty JSON format as the inverted index. Here is the expected output for the word count of all the text files associated with this project:

```json
{
	"input/text/guten/1400-0.txt": 187368,
	"input/text/guten/2701-0.txt": 215398,
	"input/text/guten/50468-0.txt": 10969,
	"input/text/guten/pg1322.txt": 124370,
	"input/text/guten/pg1661.txt": 107396,
	"input/text/guten/pg22577.txt": 63630,
	"input/text/guten/pg37134.txt": 16696,
	"input/text/rfcs/rfc3629.txt": 4294,
	"input/text/rfcs/rfc475.txt": 3228,
	"input/text/rfcs/rfc5646.txt": 27075,
	"input/text/rfcs/rfc6805.txt": 9785,
	"input/text/rfcs/rfc6838.txt": 9367,
	"input/text/rfcs/rfc7231.txt": 28811,
	"input/text/simple/.txt/hidden.txt": 1,
	"input/text/simple/a/b/c/d/subdir.txt": 1,
	"input/text/simple/animals.text": 11,
	"input/text/simple/animals_copy.text": 11,
	"input/text/simple/animals_double.text": 22,
	"input/text/simple/capital_extension.TXT": 1,
	"input/text/simple/capitals.txt": 4,
	"input/text/simple/digits.tXt": 2,
	"input/text/simple/dir.txt/findme.Txt": 17,
	"input/text/simple/hello.txt": 6,
	"input/text/simple/position.teXt": 20,
	"input/text/simple/symbols.txt": 10,
	"input/text/simple/words.tExT": 36,
	"input/text/stems/stem-in.txt": 22275,
	"input/text/stems/stem-out.txt": 22275
}
```

...and for the stand-alone `sentences.md` file:

```json
{
	"input/text/simple/sentences.md": 77
}
```
You can also find this output in the `expected/counts` subdirectory in the [`project-tests`]({{ site.github.owner_url }}/project-tests) repository.

### Query Parsing

Search queries will be provided in a text file with one multi-word search query per line. (Eventually, these queries will come from a search box on a webpage instead.) When processing this file, your query parsing code must normalize and optimize the queries as follows:

  - **Clean and parse each query line.** Perform the same transformations to each line of query words as used when populating your inverted index. This includes cleaning the line of any non-alphabetic characters, converting the remaining characters to lowercase, splitting the cleaned line into words by whitespace, and stemming each word. For example, the query line:

      ```
      Observers observing 99 HIDDEN               capybaras!
      ```

    ...should be processed into the cleaned, parsed, and stemmed words `[observ, observ, hidden, capybara]` after this step.

  - **Remove duplicate query word stems.** There is no need to search for the same stem twice! For example, if the original query included both observers and observing, the stemmed version of both words observ should be included in the parsed query only once. Specifically, for the stemmed words:

      ```
      [observ, observ, hidden, capybara]
      ```

    ...the duplicate `observ` should be removed resulting in `[observ, hidden, capybara]` after this step.

  - **Sort the unique words for each query alphabetically.** This is less necessary for the search operation, but required for the search result output. For example, if the stemmed words without duplicates are:

      ```
      [observ, hidden, capybara]
      ```

    ...then the final parsed query words should be `[capybara, hidden, observ]` after this step.

At this stage, the normalized words from the original query line can be used by your inverted index data structure to generate search results and to produce the expected JSON file output.

### Result Sorting

Search engines rank their search results such that the most useful results are provided first. For example, [PageRank](https://en.wikipedia.org/wiki/PageRank) is the well-known algorithm initially used by Google to rank results by estimating the importance of a website by its incoming links.

When returning search results, your code must also return the results in sorted order using a simple version of [term frequency](https://en.wikipedia.org/wiki/Tf%E2%80%93idf) and raw count to determine the usefulness of a result. To do this, your code will need to be able to calculate the following:

  - **Total Words:** The total number of word stems in each text file. For example, there are `6` word stems in the `hello.txt` text file. You should already have this information from the word count calculated alongside your inverted index.

  - **Total Matches:** The total number of times any of the matching query words appear in the text file.

      - For **exact search**, this is the number of times the exact word stems appear. For example, the exact word stem `perfor` appears in the file `words.tExT` a total of `2` times.

      - For **partial search**, this is the number of times a word stem *starts with* one of the query words. For example, a word stem starts with `perfor` in the file `words.tExT` a total of `11` times.

    For a query with multiple words, your code should consider *all* query words that appear at a location. For example, for an exact search of the multiple word query `[loris, okapi]`, the word stem `lori` (from `loris`) appears `3` times and the word `okapi` appears `2` times in the file `animals.text`. Therefore, the number of times any of the matching query words appear in the text file is `3 + 2 = 5` times total.

With this information you can calculate the score of the search result as the percent of words in the file that match the query. This is calculated by dividing the total matches by the total words:

```
score = total matches / total words
```

Then, when sorting the search results, compare the results as follows:

  1. **Score:** First, compare search results by their score so results with higher scores appear first (i.e. sort in descending order by total matches / total words).

  1. **Count:** If two search results have the same score, then compare by the raw count so results with higher count appear first (i.e. sort in descending order by total matches) instead.

  1. **Location:** If two search results have the same score and count, then compare by the location (case-insensitive) instead (i.e. sort alphabetically ignoring case by path).

You can use [`Double.compare(...)`](https://www.cs.usfca.edu/~cs272/javadoc/api/java.base/java/lang/Double.html#compare(double,double)), [`Integer.compare(...)`](https://www.cs.usfca.edu/~cs272/javadoc/api/java.base/java/lang/Integer.html#compare(int,int)), and [`String.compareToIgnoreCase(…)`](https://www.cs.usfca.edu/~cs272/javadoc/api/java.base/java/lang/String.html#compareToIgnoreCase(java.lang.String)) for these comparisons and the built-in sort methods in Java.

See the partial search results for `ant perf` for an example of results sorted by score, the results for `lori` for an example of results with the same score and thus sorted by count, and finally the results for `capybara hidden` for an example of results with the same score and same count and thus sorted alphabetically by location.

If you calculate the score using `float` instead of `double` objects, or sort using `Path` instead of `String` objects, you may not get the expected results!

## Input
{: .page-header }

Your `main` method must be placed in a class named `Driver`. The `Driver` class should accept the following additional command-line arguments:

  - `-counts [path]` where `-counts` is an *optional* flag that indicates the next argument `[path]` is the path to use to output all of the locations and their word count. If the `[path]` argument is not provided, use `counts.json` as the default output filename. If the `-counts` flag is not provided, do not produce an output file of locations.

  - `-query [path]` where `-query` indicates the next argument `[path]` is a path to a text file of queries to be used for search. If this flag is not provided, then no search should be performed.

  - `-exact` where `-exact` is an *optional* flag that indicates all search operations performed should be exact search. If the flag is *not* present, any search operations should use partial search instead.

  - `-results [path]` where `-results` is an *optional* flag that indicates the next argument `[path]` is the path to use for the search results output file. This may include partial or exact search results! If the `[path]` argument is not provided, use `results.json` as the default output filename. If the `-results` flag is not provided, do not produce an output file of search results but still perform the search operation.

The command-line flag/value pairs may be provided in any order, and the order provided is not the same as the order you should perform the operations (i.e. always build the index before performing search, even if the flags are provided in the other order).

Your code should support all of the command-line arguments from the [previous project](project-1.html) as well.

## Output
{: .page-header }

The output of your inverted index should be the same from the previous project. See the "Word Count" section for the desired output.

The search results should be output as a JSON array of JSON objects, where each object represents a single line from the original query file (e.g. one search). The query objects should have the cleaned, sorted query as its key and the results as its value. Specifically:

  - The key should be the quoted text value that is the parsed and sorted query words joined together by a space. For example, if the parsed query words are `[capybara, hidden, observ]` then the text output should be `"capybara hidden observ"` for the key.

  - The value should be an array of nested JSON objects, one per search result. Each individual search result should have, in order, these keys:

      - The key `count` with an integer value that is the raw count (i.e. total matches) within the text file.

      - The key `score` with a floating point value with 8 digits after the decimal point of the search result score. You can use a `DecimalFormat` object to achieve this output:

          ```java
          DecimalFormat FORMATTER = new DecimalFormat("0.00000000");
          System.out.println(FORMATTER.format(Math.PI));
          ```

        Alternatively, you can use format strings:

          ```java
          String formatted = String.format("%.8f", Math.PI);
          System.out.println(formatted);
          ```

      - The key `where` with a quoted text value that is the relative path to the text file matching one or more of the query words.


The use of spaces, newline characters, and spaces are the same as before for “pretty” JSON output. Here is an example output snippet of a single search query with a single search result:

```json
	"observ perfor": [
		{
			"count": 13,
			"score": 0.36111111,
			"where": "input/text/simple/words.tExT"
		}
	],
```

You can also find this output in the `search-exact-simple-simple.json` file in the [`project-tests`]({{ site.github.owner_url }}/project-tests) repository. See the other expected output files for more examples.

## Testing
{: .page-header }

You must pass 100% of the tests in the `Project2Test.java` group of JUnit tests in the [`project-tests`]({{ site.github.owner_url }}/project-tests) repository as reported by the "Run Project Tests" action on your project Github repository.

## Examples
{: .page-header }

The following are a few examples (non-comprehensive) to illustrate the usage of the command-line arguments that can be passed to your `Driver` class via a "Run Configuration" in Eclipse, assuming you set the working directory to the `project-tests` directory.

Consider the following example:

```
-text "input/text/simple/"
-query "input/query/simple.txt"
-exact
-results actual/search-exact-simple.json
```

The above arguments indicate that `Driver` should build an inverted index from text files in the `input/text/simple/` subdirectory of the current working directory, process the `simple.txt` query file in the `input/query` subdirectory, conduct an exact search, and output the search results to `search-exact-simple.json` in the `actual` subdirectory. This is equivalent to the `testSimpleDirectory()` test method of `Project2Test.java` in the [`project-tests`]({{ site.github.owner_url }}/project-tests) repository.

```
-text "input/text/simple/"
-query "input/query/simple.txt"
-results actual/search-exact-simple.json
```

The above arguments are nearly the same, but should trigger a partial search instead.

Note that a search should **always** be conducted if the `-query` file is provided, even if the `-results` flag is missing and no results are output to file.

## Hints
{: .page-header }

It is important to develop the project iteratively. One possible breakdown of tasks are:

  - Add the ability to **store total word count** whenever a file is indexed, and the ability to output these counts when the `-counts` flag is provided.

  - Add the ability to **parse query files**. Compare your parsed queries to those in the expected output files. For example, the line `performer performers` should become `perform` after being parsed, cleaned, stemmed, sorted, and discarding duplicates.

  - Create a class that stores a **single search result** and implements the [Comparable](hhttps://www.cs.usfca.edu/~cs272/javadoc/api/java.base/java/lang/Comparable.html) interface. You will need data members for each of the sort criteria, including the location, total word count of the location, and number of times the query occurs at that location. This is similar to the `TextFileSorter` homework assignment.

  - Add an **exact search method** to your inverted index data structure that takes already parsed words from a single line of the query file, and returns a sorted list of search results. Output the results to the console for debugging.

      <i class="fas fa-exclamation-triangle"></i>
      Use lists and <a href="https://www.cs.usfca.edu/~cs272/javadoc/api/java.base/java/util/Collections.html#sort(java.util.List)">Collections.sort(List)</a> to sort search results, not a <a href="https://www.cs.usfca.edu/~cs272/javadoc/api/java.base/java/util/TreeSet.html">TreeSet</a> data structure. Custom mutable objects do not behave well when used in sets or as keys in maps.
      {: .notification .is-warning }

  - Add the ability to **output the search results** to JSON file. Make sure the exact search results match the expected output.

  - Add a **partial search method** to your inverted index data structure that takes already parsed words from a single line of the query file, and returns a sorted list of search results.

  - Do not worry about efficient partial search until after you are getting correct results.

The important part will be to test your code as you go. The JUnit tests provided only test the entire project as a whole, not the individual parts. You are responsible for testing the individual parts themselves.

<i class="fas fa-info-circle"></i>
These hints may or may not be useful depending on your approach. Do not be overly concerned if you do not find these hints helpful for your approach for this project.
{: .notification }

{% endcomment %}
