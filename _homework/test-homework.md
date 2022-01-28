---
layout: guides
navbar: Guides
title: Testing Homework
key: 3

example_test: 'https://github.com/usf-cs272-spring2022/homework-ArgumentParser-template/blob/01d2c51a1986ee4007ad0a040fe6ffbdc9641cb1/src/test/java/edu/usfca/cs272/ArgumentParserTest.java#L73-L86'
example_run: 'https://github.com/usf-cs272-spring2022/homework-ArgumentParser-template/runs/4985351349?check_suite_focus=true#step:3:1'

---

Every homework comes with a `src` » `test` » `java` directory with JUnit 5 test code. You must pass all of these tests remotely to earn full credit.

<i class="fas fa-info-circle"></i>
The screenshots are shown at reduced size. Click to open the image to view it at 100% size (useful for reading the text).
{: .notification }

## Understanding Tests
{: .page-header }

Each homework will have a class called `HomeworkTest.java` where `Homework` is the name of the homework assignment. For example, for the `ArgumentParser` homework, its associated test class is `ArgumentParserTest.java`.

The homework tests use the [Junit 5](https://junit.org/junit5/) testing framework, which has built-in support in Eclipse. The tests themselves are Java code. There are always several parts of a test: the test case (method being tested and on which input), the actual result of running that method, and the expected result.

For example, consider [this test]({{ page.example_test }}):

```java
/**
 * Tests values that should be considered invalid flags.
 *
 * @param flag invalid flag value
 */
@Order(2)
@ParameterizedTest(name = "[{index}: \"{0}\"]")
@ValueSource(strings = { "a-b-c", "hello", "hello world", "", " ", "\t",
    "\n", "-", " - a", " -a", "\t-a", "--a", "-$a", "-_a", "-\ta", "97",
    "1", "-1", "-42" })
public void testInvalidFlags(String flag) {
  boolean actual = ArgumentParser.isFlag(flag);
  Assertions.assertFalse(actual, flag);
}
```

The method being tested is the `isFlag` method in `ArgumentParser`, given by this line:

```java
boolean actual = ArgumentParser.isFlag(flag);
```

The method is being tested multiple times, once for each input in the `@ValueSource` here:

```java
@ValueSource(strings = {
    "a-b-c", "hello", "hello world", "", " ", "\t", "\n", "-", " - a",
    " -a", "\t-a", "--a", "-$a", "-_a", "-\ta", "97", "1", "-1"
})
```

For each of these input values for the `isFlag` method, the test is expecting the method to return `false` each time:

```java
Assertions.assertFalse(actual, flag);
```

If we consider the first input value, then the code *asserts* `ArgumentParser.isFlag("a-b-c")` should return `false`. If it does, the test passes. If not, an exception is thrown.

Each method might look slightly different, but it will always have those same three components: what is being tested, what is the actual value, and what is the expected value. If you ever have trouble understanding a test, reach out on CampusWire!

## Local Testing
{: .page-header }

**You should try passing the tests locally before you try passing them remotely.** Before you can do that, you need to follow the [setup homework](/guides/homework/setup-homework.html) guide to setup the your repository using Github classroom and then import that repository as a Java Project in Eclipse.

To run the JUnit tests provided with the homework template, follow these steps:

  1. Open up the `src` » `test` » `java` subfolder in the Eclipse project.

  2. Open up the class containing the same name as the homework assignment plus the suffix `Test` at the end. For example, for the `ArgumentParser` homework assignment, `ArgumentParserTest` is the associated test class.

  3. From the "Run" menu, select "Run As" &raquo; "JUnit Test" from the menu. If prompted which tests to run, select the one with the same name as the class. For example, for the `ArgumentParser` homework assignment, `ArgumentParserTest` is the associated test class.

  4. Running the tests should open the "JUnit" view. You can use that view to see which tests you are passing and which you are not. See the [Eclipse User Guide](https://help.eclipse.org/latest/topic/org.eclipse.jdt.doc.user/reference/views/ref-view-junit.htm) for what each of the buttons mean in this view.

  5. After making changes to your code, you can re-run the tests by following the same steps or clicking the <img alt="Rerun Test" src="https://help.eclipse.org/latest/topic/org.eclipse.jdt.doc.user/images/org.eclipse.jdt.junit/elcl16/relaunch.svg"> Rerun Test button.

It is important you only try to pass one test at a time, because the changes you make may affect other tests. You should commit your changes every time you start passing a new test. You only need to push your changes at the end of every coding session (you can do it more often as well).

#### Running Individual Tests

While you are initially working on a homework assignment, you should focus on individual tests or individual groups of tests. There is no need to run *all* of the tests every time; in fact this can make debugging harder!

Focus on the tests in the order they are provided in the test class. Run the first group of tests in the file and focus on the first individual test that is not passing. Once that is passing, run the group of tests again and repeat the same process. It is common that fixing an issue for one test will cause other tests to pass or fail, so it is important to work iteratively and re-run the tests often.

There are *many* ways to run an individual JUnit test within Eclipse. Here are a few options:

  - Open up the test file in the Java perspective. Find the test in the "Outline" view. Right-click the name, and select "Run As" then "JUnit Test" from the menus.

      [![Screenshot]({{ "/images/eclipse-run-one-from-outline.png" | relative_url }}){: .is-400}]({{ "/images/eclipse-run-one-from-outline.png" | relative_url }})

  - In the JUnit view, right-click the test you want to run and select "Run" from the menu. ([See example.]({{ "/images/eclipse-run-one-from-junit.png" | relative_url }}))

  - In the "Package Explorer" view, browse to the test, right-click the test name, and select "Run As" then "JUnit Test" from the menus. ([See example.]({{ "/images/eclipse-run-one-from-explorer.png" | relative_url }}))

  - Open up the test file in the Java perspective. Find the test in the file. Click the test so it is the current active line in the editor. Right-click the name, and select "Run As" then "JUnit Test" from the menus. ([See example.]({{ "/images/eclipse-run-one-from-file.png" | relative_url }}))

  - Finally, if you want to manually run a single test (or group of tests), you can modify the run configuration to look something like this:

      [![Screenshot]({{ "/images/eclipse-run-one-from-configuration.png" | relative_url }}){: .is-600}]({{ "/images/eclipse-run-one-from-configuration.png" | relative_url }})

Pretty much anywhere you can find the test and right-click it, you can run it as a JUnit test without running everything else. This process works for an individual test method or a group of tests (usually an inner or nested class with multiple test methods)!

#### Advanced: Running Tests via Maven

If you want to be sure there are no surprises when your code is tested by Github Actions, you need to run the [Maven](https://maven.apache.org/) command in Eclipse. Maven is the tool being used to setup your Eclipse projects (it handles importing third-party packages and the compile settings), and it is the tool used by Github Actions to compile and test your code.

<details>
<p><summary>View Details</summary></p>

<div markdown=1>

Most of the homework assignments assign 5 points for having warning-free code. Maven uses a different compiler than Eclipse, so you might not see the same set warnings reported in the "Problems" view of Eclipse that will be caught when Maven is run by Github Actions. To check for warnings, follow these steps:

  1. Right-click the `pom.xml` file, open the "Run As" menu, and select "3 Maven build..." from the menu. Make sure to select the option with the `...` at the end.

      [![Screenshot]({{ "/images/eclipse-runas-maven.png" | relative_url }}){: .is-400 }]({{ "/images/eclipse-runas-maven.png" | relative_url }})

  2. On the resulting popup window, make sure to enter `clean compile` into the "Goals" text box.

  3. Click the "Add..." button and add a parameter with name `compileOptionFail` and value `true`. This will cause the compile operation to fail if there are warnings in your code.

      [![Screenshot]({{ "/images/eclipse-maven-warnings.png" | relative_url }}){: .is-400 }]({{ "/images/eclipse-maven-warnings.png" | relative_url }})

  4. Click the "Run" button and inspect the console output. If you see this message:

      ```
      [ERROR] error: warnings found and -Werror specified
      ```

      That means there was a warning and your code failed to compile. If you scroll up, you should find a heading:

      ```
      [WARNING] COMPILATION WARNING :
      ```

      ...and underneath there you will find the warning messages. Fix those before moving on.

The next step is to re-compile your code regardless of warnings. Follow the same steps as above to open the "Maven build..." menu. In the popup window, make sure to enter:

  1. Enter `clean compile test-compile` in the "Goals" text box. (Note the addition of `test-compile` this time.)

  2. Make sure there are NO parameters provided.

  3. Click the "Run" button and inspect the console output. Ignore the `SLF4J` output at the start. If you see this message:

      ```
      [INFO] BUILD SUCCESS
      ```

      ...then the compile was successful and you can move on to the next step. If this does not work, reach out to us on CampusWire for help.

Finally, you can run the tests as they will be run by Github Actions.  Follow the same steps as before to open the "Maven build..." menu. In the popup window, make sure to enter:

  1. Enter `test` in the "Goals" text box.

  2. Click the "Add..." button and add a parameter with name `test` and value `HomeworkTest*` where `Homework` is the homework name. For example, enter `ArgumentParserTest*` to run all of the tests for the `ArgumentParser` homework.

      Alternatively, if you want to run one of the A, B, C, etc. test groups, enter `HomeworkTest*X_*` where `Homework` is the homework name and `X` is the test group (such as `A`, `B`, and so on). For example, enter `ArgumentParserTest*A_*` to run the `A` tests for the `ArgumentParser` homework.

      [![Screenshot]({{ "/images/eclipse-maven-run-test.png" | relative_url }}){: .is-400 }]({{ "/images/eclipse-maven-run-test.png" | relative_url }})

  3. Click the "Run" button and inspect the console output for which tests passed or failed.


If you see error messages similar to these in your console:

<pre class="has-text-danger">
SLF4J: Class path contains multiple SLF4J bindings.
SLF4J: Found binding in [...StaticLoggerBinder.class]
SLF4J: Found binding in [...StaticLoggerBinder.class]
SLF4J: See http://www.slf4j.org/codes.html#multiple_bindings for an explanation.
SLF4J: Actual binding is of type [org.slf4j.impl.SimpleLoggerFactory]
</pre>

While the messages are *annoying*, they do not impact your code. However, [you can remove them](https://stackoverflow.com/questions/63518376/eclipse-maven-slf4j-class-path-contains-multiple-slf4j-bindings) by doing the following:

  1. Open the "About Eclipse" dialog from the "Eclipse" menu and click the "Installation Details" button.

      ![Screenshot]({{ "/images/eclipse-about.png" | relative_url }}){: .is-400 }

  2. In the "Installed Software" tab, select "m2e - slf4j over logback logging (Optional)" and then click "Uninstall".

      ![Screenshot]({{ "/images/eclipse-installed-software.png" | relative_url }}){: .is-400 }

After that is uninstalled, you should no longer see that error message.
</div>
</details>

<br/>
Generally these steps are only necessary if your tests pass normally in Eclipse but not on Github Actions. It is easier to debug the issue locally than re-run the Github Action multiple times.

## Remote Testing
{: .page-header }

Once you are passing all of the tests locally, it is time to test your homework remotely.

  1. AFTER you have made a commit and pushed it to Github, open up your repository on Github. You should be able to see the status of your commit:

      [![Screenshot]({{ "/images/github-commit-status.png" | relative_url }}){: .is-400 }]({{ "/images/github-commit-status.png" | relative_url }})

      There are three icons you could see next to your commit:

        - <i class="far fa-check fa-fw has-text-success"></i> A green checkmark means the autograder ran successfully and everything passed. Nice work!
        - <i class="fas fa-circle fa-fw has-text-warning"></i> A yellow dot means the autograder is not yet done running.
        - <i class="far fa-times fa-fw has-text-danger"></i> A red "x" means the autograder ran but one or more of the tests did not pass. In this case, you'll need to look at the details to see why.

      If the autograder is still running, you can go look at the details or refresh once it is done to see the status.

  2. On that same page, you should also see the number of points you are earning for the homework assignment:

      [![Screenshot]({{ "/images/homework-readme.png" | relative_url }}){: .is-400 }]({{ "/images/homework-readme.png" | relative_url }})

      Keep in mind that the number of points displayed in your `README` will not be correct until the autograder is complete. If you see the yellow dot next to your commit, you'll need to refresh the `README` file when it is done to see the updated value.

  3. If you want more details, you have to click on the "Actions" tab. From there, you should see all of the autograder runs. Click on the latest run for details.

      [![Screenshot]({{ "/images/github-workflow-status.png" | relative_url }}){: .is-400 }]({{ "/images/github-workflow-status.png" | relative_url }})

  4. The workflow details view will show you the status of each step, but the only really important one is the "Autograding" step. You can also see the number of points warned in the "Annotations" section:

      [![Screenshot]({{ "/images/github-homework-action-summary.png" | relative_url }}){: .is-400 }]({{ "/images/github-homework-action-summary.png" | relative_url }})

      Github will often add other warnings here related to the Github Actions infrastructure. You can usually ignore those.

  5. Click on the "Autograding" action for details on which tests passed or failed. There is a lot of output to scroll through here. For example:

      [![Screenshot]({{ "/images/github-homework-action-detail.png" | relative_url }}){: .is-400 }]({{ "/images/github-homework-action-detail.png" | relative_url }})

      ...the "📝 Check Commit Count" heading is the start of that test output. The "❌ Check Commit Count" heading is the end of that output with the status of that test. Everything in between those two headings is the output from Maven for that test.

      In this case, the ❌ red "x" means the test failed. You will see a ✅ green checkmark if the test passed.

      **Ignore the line that states:**

      <pre class="has-text-warning">
      Warning: G] Unable to autodetect 'javac' path, using 'javac' from the environment.</pre>

      ...this is output by Maven and not an issue with your code.

You can link to a specific line in this autograder run when asking for help on [Piazza]({{ site.data.info.links.forums.link }})! For example, [here is a link]({{ page.example_run }}) to the autograder run for the `ArgumentParser` template.
