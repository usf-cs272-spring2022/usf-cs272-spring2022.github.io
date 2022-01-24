---
title: Project 1 Inverted Index
navbar: Guides
layout: guides
key: 1.0
bump: true

assignments:
  - text: 'Project 1 Functionality'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118291'

  - text: 'Project 1 Design'
    link: 'https://usfca.instructure.com/courses/1602551/assignments/7118297'

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

  - Create a custom **inverted index** data structure that stores a mapping from a word stem to the location(s) the word was found, and the position(s) in that file the word is located. The positions should start at 1. *This will require nesting multiple built-in data structures.*

  - If provided a directory as input, find all files within that directory and all subdirectories and parse each text file found. Any files that end in the `.text` or `.txt` extension (case insensitive) should be considered a text file. If provided a single file as input, only parse that individual file (regardless of its extension).

      - Use the `UTF-8` character encoding for all file processing, including reading and writing.

  - Process text into word stems by removing any non-letter symbols (including digits, punctuation, accents, special characters), convert the remaining alphabetic characters to lowercase, split the text into words by whitespace, and then stem the word using the [Apache OpenNLP](https://opennlp.apache.org/) toolkit.

      - Use the regular expression `(?U)[^\\p{Alpha}\\p{Space}]+` to remove special characters from text.

      - Use the regular expression `(?U)\\p{Space}+` to split text into words by whitespace.

      - Use the [SnowballStemmer](https://opennlp.apache.org/docs/1.9.3/apidocs/opennlp-tools/opennlp/tools/stemmer/snowball/SnowballStemmer.html) English stemming algorithm in OpenNLP to stem words.

  - If the appropriate command-line arguments are provided, output the inverted index in pretty [JSON](https://en.wikipedia.org/wiki/JSON) format using tab characters. See the "Output" section below for specifics.

  - Output user-friendly error messages in the case of exceptions or invalid input. Under no circumstance should your `main()` method output a stack trace to the user!

The functionality of your project will be evaluated with the `Project1Test.java` group of JUnit tests. See the "Testing" section for details.

## Input
{: .page-header }

Your `main` method must be placed in a class named `Driver`. The `Driver` class should accept the following command-line arguments:

  - `-text [path]` where the flag `-text` indicates the next argument `[path]` is a path to either a single file or a directory. If the value is a file, open and process that file regardless of its extension. If the value is a directory, find and process all of the text files (with `.txt` and `.text` extensions) in that directory and its subdirectories.

  - `-index [path]` where the flag `-index` is an *optional* flag that indicates the next argument `[path]` is the path to use for the inverted index output file. If the path argument is not provided, use `index.json` as the default output path. If the `-index` flag is provided, always generate output even if it is empty. If the `-index` flag is not provided, do not produce an output file.

The command-line flag/value pairs may be provided in any order. Do not convert paths to absolute form when processing command-line input!

## Output
{: .page-header }

All output will be produced in "pretty" JSON format using `\t` tab characters for indentation. According to the [JSON standard](http://json.org/), numbers like integers should never be quoted. Any string or object key, however, should always be surrounded by `"` quotes. Objects (similar to maps) should use `{` and `}` curly braces, and arrays should use `[` and `]` square brackets. Make sure there are no trailing commas after the last element.

The paths should be output in the form they were originally provided. The tests use normalized relative paths, so the output should also be normalized relative paths. As long as command-line parameters are not converted to absolute form, this should be the default output provided by the path object.

The contents of your inverted index should be output in alphabetically sorted order as a nested JSON object using a “pretty” format. For example:

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

The project tests account for different path separators (forward slash `/` for Linux/Mac systems, and backward slash `\` for Windows systems). Your code does *not* have to convert between the two!

## Testing
{: .page-header }

You must pass 100% of the tests in the `Project1Test.java` group of JUnit tests in the [`project-tests`]({{ site.github.owner_url }}/project-tests) repository as reported by the "Run Project Tests" action on your project Github repository.

## Examples
{: .page-header }

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

## Hints
{: .page-header }

It is important to **develop the project iteratively**. In fact, you may already have certain components complete thanks to the homework assignments. One possible breakdown of tasks are:

  - Create code that handles parsing command-line arguments into flag/value pairs, and supports default values if a flag is missing a value. This is similar functionality as your `ArgumentMap` homework assignment.

  - Create code that is able to traverse a directory and return a list of all the text files found within that directory. The File I/O [lecture code](https://github.com/usf-cs272-fall2021/lectures/tree/main/FileIO) or [Java tutorials](https://docs.oracle.com/javase/tutorial/essential/io/fileio.html) might be useful for this. This is also similar functionality as your `TextFileFinder` homework assignment.

  - Create code that is able to parse text into words, including converting that text to lowercase, replacing special characters and digits, splitting that text into words by whitespaces, and finally stemming the words. This is similar functionality as your `TextFileStemmer` homework assignment.

  - Create code that handles storing a word, file path, and location into an inverted index data structure. This is similar functionality (but not exactly the same) as your `TextFileIndex` homework assignment. (In particular, you do not want to directly reuse the `ForwardIndex` interface. However, the design could be similar.)

  - Create code that is capable of writing a nested data structure (matching your inverted index data structure) to a file in JSON format. This is similar functionality as your `SimpleJsonWriter` homework assignment.

Test each part of your project code. Keep in mind the tests provided only test the final output of your Java program. **You are responsible for testing the individual components of your code.**

You can use and modify homework assignments for this project. However, make sure they are passing all of the tests before using.

Once you have the above components working, then you can work on integrating your code together. This part must still be done iteratively! Do not try to combine all of the code at once. First, work on being able to traverse a directory based on command-line parameters. Then, clean the text files found and output the cleaned words to the console. Finally, add those words to the index and write that index as JSON.

<i class="fas fa-info-circle"></i>&nbsp;These hints may or may not be useful depending on your approach. Do not be overly concerned if you do not find these hints helpful for your approach for this project.
{: .notification }
