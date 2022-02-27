
Use these steps to make practice quizzes from assignment quizzes.

  1. **Export quizzes:** Go to "Settings" » "Export Course Content" and select "Quiz" as the export type. Select the quizzes you wish to duplicate into practice versions, and download the ZIP file.

  1. **Extract export:** Extract the ZIP export and open the folder as a project in Atom.

  1. **Change title:** Use the "Find in Project" feature **with Regex** enabled and search for the regex:

    ```regex
    <title>(.+?)</title>
    ```

    And replace it with:

    ```regex
    <title>$1 (Practice)</title>
    ```

    Next, with regex enabled, search for the regex:

    ```regex
    <assessment (.+?) title="(.+)">
    ```

    And replace it with:

    ```regex
    <assessment $1 title="$2 (Practice)">
    ```

  1. **Change type:** Use the "Find in Project" feature and search for:

      ```xml
      <quiz_type>assignment</quiz_type>
      ```

      And replace it with:

      ```xml
      <quiz_type>practice_quiz</quiz_type>
      ```

  1. **Change visibility:** If you want to change the visibility of the assignment, use the "Find in Project" feature and search for:

      ```xml
      <available>true</available>
      ```

      And replace it with:

      ```xml
      <available>false</available>
      ```

      And search for:

      ```xml
      <workflow_state>published</workflow_state>
      ```

      And replace it with:

      ```xml
      <workflow_state>unpublished</workflow_state>
      ```

      These steps can be skipped if you do not want to change the visibility.

  1. **Create archive:** Using your favorite tool, create a new ZIP file with the modified quizzes.

  1. **Import archive:** Go to "Settings" » "Import Course Content" and select "Canvas Course Export Package" from the dropdown. Upload the ZIP file you just created.

  1.
