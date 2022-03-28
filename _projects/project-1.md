---
title: Project 1 Inverted Index
navbar: Guides
layout: guides
key: 1.0
bump: true
project: 1

#tags:
#  - text: 'New'
#    type: 'is-primary'

assignments:
  - text: 'Project 1 Tests'
    link: 'https://usfca.instructure.com/courses/1605147/assignments/7166795'

  - text: 'Project 1 Review 1'
    link: 'https://usfca.instructure.com/courses/1605147/assignments/7166797'

  - text: 'Project 1 Review 2'
    link: 'https://usfca.instructure.com/courses/1605147/assignments/7166798'

  - text: 'Project 1 Final Release'
    link: 'https://usfca.instructure.com/courses/1605147/assignments/7166799'

---

For this project, you will write a Java program that processes all text files in a directory and its subdirectories, cleans and parses the text into [word stems](https://en.wikipedia.org/wiki/Stemming), and builds an in-memory [inverted index](https://en.wikipedia.org/wiki/Inverted_index) to store the mapping from word stems to the documents and position within those documents where those word stems were found.

For example, suppose we have the following mapping stored in our inverted index:

```json
{
	"capybara": {
		"input/mammals.txt": [
			11
		]
	},
	"platypus": {
		"input/dangerous/venomous.txt": [
			2
		],
		"input/mammals.txt": [
			3,
			8
		]
	}
}
```

This indicates that after processing the word stems from files, the word `capybara` is found in the file `input/mammals.html` in position `11`. The word `platypus` is found in two files, `input/mammals.html` and `input/dangerous/venomous.html`. In the file `input/mammals.html`, the word `platypus` appears twice in positions `3` and `8`. In file `input/dangerous/venomous.html`, the word `platypus` is in position `2` in the file.

The process of stemming reduces a word to a base form (or "stem"), so that words like `interesting`, `interested`, and `interests` all map to the stem `interest`. Stemming is a common preprocessing step in many web search engines.

## Functionality
{: .page-header }

The core functionality of your project must satisfy the following requirements:

  - Process command-line arguments to determine the input to process and output to produce. See the "Input" and "Output" sections below for specifics.

  - If provided a single file as input, only parse that individual file (regardless of its extension). If provided a directory as input, find all files within that directory and all subdirectories and parse each text file found.

      - Any files that end in the `.text` or `.txt` extension (case insensitive) should be considered a text file.

      - Use the `UTF-8` character encoding for all file processing, including reading and writing.

  - Parse text into word stems by removing any non-letter symbols (including digits, punctuation, accents, special characters), convert the remaining alphabetic characters to lowercase, split the text into words by whitespace, and then stem the word using the [Apache OpenNLP](https://opennlp.apache.org/) toolkit.

      - Use the regular expression `(?U)[^\\p{Alpha}\\p{Space}]+` to remove special characters from text.

      - Use the regular expression `(?U)\\p{Space}+` to split text into words by whitespace.

      - Use the [SnowballStemmer](https://opennlp.apache.org/docs/1.9.3/apidocs/opennlp-tools/opennlp/tools/stemmer/snowball/SnowballStemmer.html) English stemming algorithm in OpenNLP to stem words.

  - Create a custom **inverted index** data structure that stores a mapping from a word stem to the location(s) the word was found, and the position(s) in that file the word is located. The positions should start at 1. *This will require nesting multiple built-in data structures.*

  - If the appropriate command-line arguments are provided, output the inverted index in pretty [JSON](https://en.wikipedia.org/wiki/JSON) format using tab characters. See the "Output" section below for specifics.

  - Output user-friendly error messages in the case of exceptions or invalid input. Under no circumstance should your `main()` method output a stack trace to the user!

See the following sections for additional details.

### Input

Your `main` method must be placed in a class named `Driver` and must process the following command-line arguments:

  - `-text [path]` where the flag `-text` indicates the next argument `[path]` is a path to either a single file or a directory.

      If the value is a file, open and process that file regardless of its extension. If the value is a directory, find and process all of the text files (with `.txt` and `.text` extensions) in that directory and its subdirectories.

  - `-index [path]` where the flag `-index` is an *optional* flag that indicates the next argument `[path]` is the path to use for the inverted index output file.

      If the path argument is not provided, use `index.json` as the default output path. If the `-index` flag is provided, always generate output even if it is empty. If the `-index` flag is not provided, do not produce an output file.

The command-line flag/value pairs may be provided in any order. Do not convert paths to absolute form when processing command-line input!

### Output

The contents of your inverted index should be output in alphabetically sorted order as a nested JSON object using a "pretty" format using `\t` tab characters for indentation.

According to the [JSON standard](http://json.org/), numbers like integers should never be quoted. Any string or object key, however, should always be surrounded by `"` quotes. Objects (similar to maps) should use `{` and `}` curly braces, and arrays should use `[` and `]` square brackets. Make sure there are no trailing commas after the last element. For example:

```json
{
	"capybara": {
		"input/mammals.txt": [
			11
		]
	},
	"platypus": {
		"input/dangerous/venomous.txt": [
			2
		],
		"input/mammals.txt": [
			3,
			8
		]
	}
}
```

The paths should be output in the form they were originally provided. The tests use normalized relative paths, so the output should also be normalized relative paths. As long as command-line parameters are not converted to absolute form, this should be the default output provided by the path object.

The project tests account for different path separators (forward slash `/` for Linux/Mac systems, and backward slash `\` for Windows systems). Your code does *not* have to convert between the two!

## Grading
{: .page-header }

The following sections detail how to earn credit for this project. The project grade is separated into one "functionality" or "test" grade worth 100 points, and a series of "design" or "code review" grades that together are worth another 100 points.

#### Project Tests

To be eligible for the "Project {{ page.project }} Tests" grade, you must meet the following criteria:

  - Your code must pass the tests for the current project, project {{ page.project }}.

  - Your code must *not* pass the tests for the future project, [project {{ page.project | plus: 1 }}](project-{{ page.project | plus: 1 }}.html).

The tests for this project can be found in the `Project{{ page.project }}Test.java` group of JUnit tests in the [`project-tests`]({{ site.github.owner_url }}/project-tests) repository. See the [Project Testing](project-testing.html) guide for additional details.

#### Project Reviews

To be eligible for the "Project {{ page.project }} Review 1" grade, you must meet the following criteria:

  - You must have a non-zero grade for the "Project {{ page.project }} Tests" assignment in Canvas and your code must still pass the associated tests.

  - Your code must additionally pass the code review checks, and you must attend a code review with the instructor.

See the [Project Reviewing](project-reviewing.html) guide for additional details, including how to earn the subsequent "Project {{ page.project }} Review 2" and "Project {{ page.project }} Final Release" grades.

## Getting Started
{: .page-header }

The following sections may be useful for getting started on this project.

### Examples

The following are a few examples (non-comprehensive) to illustrate the usage of the command-line arguments that can be passed to your `Driver` class via a "Run Configuration" in Eclipse, assuming you set the working directory to the `project-tests` directory.

Consider the following example:

```
-text "input/text/simple/hello.txt"
-index "actual/index-simple-hello.json"
```

The above arguments indicate that `Driver` should build an inverted index from the single `hello.txt` file in the `input/text/simple` subdirectory of the current working directory, and output the inverted index as JSON to the `index-simple-hello.json` file in the `actual` subdirectory.

```
-text "input/text/simple/" -index
```

The above arguments indicate that `Driver` should build an inverted index from all of the text files found in the `text/simple` subdirectory of the current working directory, and output the inverted index as JSON to the default path `index.json` in the current working directory.

```
-text "input/text/simple/"
```

The above arguments indicate that `Driver` should build an inverted index from all of the text files found in the `input/text/simple` subdirectory of the current working directory, but it should *not* produce an output file. It must still build the inverted index however! (This will be useful in the future when we add the ability to search.)

```
-index
```

The above arguments indicate that `Driver` should output the inverted index as JSON to the default path `index.json` in the current working directory. The inverted index will be empty, since no `-path` flag argument was provided.

### Related Content

The following homework assignments and lecture code may be useful to complete as part of this project:

  - The `ArgumentParser` homework is useful for processing the command-line arguments. This homework can be used directly for your project.

  - The `TextFileStemmer` homework is useful for converting text files into word stems. This homework can be used directly for your project.

  - The `SimpleJsonWriter` homework is useful for producing pretty JSON output. This homework can be used directly and extended as needed for your project.

  - The `TextFileIndex` homework is useful as an example for designing a data structure like an inverted index. Other examples are provided in the object-oriented programming lectures. This homework should *not* be used directly for your project; a forward index has a different underlying structure than an inverted index.

  - The `TextFileFinder` homework is useful for listing all of the text files in a directory using functional programming. This can also be done without functional programming using examples from the file IO lectures.

  - The lectures on exception handling, file IO, data structures, and object-oriented programming may be helpful for completing this project. The lectures on inheritance and functional programming may also be helpful, but are not required for core functionality.

You can modify homework assignments and lecture code as necessary for this project. However, for homework, make sure your code is passing all of the tests before using.

You should *not* wait until you have completed all of the associated homework assignments or covered all of the related lecture content to start the project. You should **develop the project iteratively** as you progress throughout the semester, integrating assignments and concepts one at a time into your project code.

### Hints

Your goal should be to get to testable code as quickly as possible first, and then to focus on passing the functionality tests. One possible breakdown of tasks are:

  1. Figure out how to run tests *individually* and focus only on the first test method until that test passes.

  2. Create code that handles parsing command-line arguments for the first test. Output the parsed arguments to the console.

  3. Create code that is able to parse the single text file specified by the first test into word stems. Output the stems to the console.

  4. Create code that is able to write the word stems to the JSON file specified by the first test. Do not worry about the data structure or format of the output file yet.

  5. Compare the actual output file produced by your code to the expected file. While the output format will not match, you want to check the same stems are found in both files.

You now have testable code at this point. Keep in mind the tests provided only test the final output of your Java program. **You are responsible for testing the individual components of your code.**

Once you have testable code, try working on the following:

  {:start="6"}
  6. Create the data structure that will store your inverted index.

  7. Create code to output your data structure to file, but not yet in the right format. Check that the word stems, path locations, and word positions match the expected output.

  8. Create code to output your data structure to file in proper "pretty" JSON format.

Start trying to pass all of the single file tests. Do not move on until the tests for single files are passing. Then, try the following:

  {:start="8"}
  8. Create code to find all of the text files in a directory.

  9. Create code (ideally reusing what you already have) to process the text files into your inverted index data structure.

Then, start trying to pass the directory tests. Do not move on until those tests are passing. Finally, work on the exception tests *last* after everything else is passing.

It is important to **get started early** so you have plenty of time to think about how you want to approach the project *and* start coding iteratively. Planning to complete the code in too large of a chunk is a recipe to get stuck and fall behind!

<i class="fas fa-info-circle"></i>&nbsp;These hints may or may not be useful depending on your approach. Do not be overly concerned if you do not find these hints helpful for your approach for this project.
{: .notification }
