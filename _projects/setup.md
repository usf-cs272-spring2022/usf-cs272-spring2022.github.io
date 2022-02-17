---
title: Project Setup
navbar: Guides
layout: guides
key: 0.1

#tags:
#  - text: 'New'
#    type: 'is-primary'
---

The project is broken into two separate Github repositories and Eclipse projects:

  - **SearchEngine**: This is where you will place your project code. You will have your own private version of this project. The initial template includes some configuration files and a skeleton `Driver.java` class.

  - **SearchEngineTest**: This is where the project tests files and expected output files are located. Everyone shares the same read-only repository. It will start with the [Project 1](project-1.html) test files first and will be updated throughout the semester with new test files for the other projects.

You will reuse these repositories for all of the projects.

When we verify the functionality and review the design of your project, we will only checkout the **SearchEngine** repository each time. This helps avoid having to re-copy the large test files over and over again.

## Walkthrough Video

You can find a walkthrough video of these steps here:

<figure>
<p>
  <iframe src="https://drive.google.com/file/d/14oecs2WIJrRQJnWnRlKE2-4nt2lZa5vW/preview" width="640" height="360" allow="autoplay" class="is-bordered"></iframe>
  <br/>
  <caption><a href="https://drive.google.com/file/d/14oecs2WIJrRQJnWnRlKE2-4nt2lZa5vW/view?usp=sharing">https://drive.google.com/file/d/14oecs2WIJrRQJnWnRlKE2-4nt2lZa5vW/view?usp=sharing</a></caption>
</p>
</figure>

The version of Java and appearance of Eclipse may be slightly different between semesters.

## Create and Import Projects

Below is a quick summary of the **one-time setup** needed for the project:

  1. Visit the [Project Setup](https://usfca.instructure.com/courses/1605147/assignments/7184853) assignment in Canvas and click the Github Classroom link. This will setup a private repository named `project-username` where `username` is your Github username. You will use this same repository the *entire* semester for all of the projects.

  1. Import the repository as a Java Project in Eclipse. See the [Importing Eclipse Projects from Github](/guides/eclipse/importing-eclipse-projects-from-github.html) guide for steps. This will create a "SearchEngine" project in Eclipse where you will add your own code for the project.

  1. Import the `project-tests` repository at <{{ site.data.info.links.github.link }}/project-tests> as a Java Project in Eclipse. This will create a "SearchEngineTests" project in Eclipse where you will find all of the test code and data files.

      <i class="fas fa-exclaimation-triangle"></i>&nbsp;**These two projects must be located in the same parent directory!** For example `repos/project-username` and `repos/project-tests` share the same parent directory `repos`.

  1. If there are compile issues, right-click the "SearchEngine" project in your "Package Explorer" view, go to the "Maven" menu, and select "Update Project..." from the submenu. Make sure "SearchEngine" is selected and click the "OK" button.

After importing into Eclipse, the "Package Explorer" view should look *similar* to this:

![Screenshot]({{ "/images/project-eclipse.png" | relative_url }}){: style="width: 250px;" class="is-size is-bordered" }

Important files or directories are highlighted in blue. Your view will not have this highlighting. You may also be missing the `actual` folder until your project is producing output files.

**Once setup, you do not need to go through these steps again.**

## Verify Setup

Once you have everything imported into Eclipse, try these steps to verify everything is setup correctly:

  1. Verify you can run the `Project1Tests.java` set of tests in the "SearchEngineTests" project in Eclipse.

  1. Verify you can make, commit, and push changes to `Driver.java` in the "SearchEngine" project in Eclipse.

  1. Create your first release. Click the "Releases" heading (usually on the right side) in Github and click the "Draft a new release" button. Enter `v1.0.0` as the tag version, *optionally* click the "This is a pre-release" checkbox, and leave the other fields unchanged:

      ![Screenshot]({{ "/images/github-create-release.png" | relative_url }}){: .is-400 }

      There is an [example release]({{ site.data.info.links.github.link }}/project-template/releases/tag/v1.0.0) in the `project-template` repository.

  1. Go to the "Actions" tab and make sure the "Check project release" workflow ran for the `v1.0.0` release. There is an [example run]({{ site.data.info.links.github.link }}/project-template/actions/workflows/project-release.yml) in the `project-template` repository. It *should* fail, since you don't have any code yet.

If you are able to complete all of the above, you should be ready to start your project! More about releases and the workflow output can be found in the [Project Testing](testing.html) guide.

## Folder Structure

Here is the folder structure for the project and its tests:

```
├── SearchEngine (project-username)
│   ├── pom.xml (should not need modification)
│   ├── src/main/java/edu/usfca/cs272
│   │   ├── Driver.java (modify as needed)
│   │   └── (add other *.java files here)
│   └── src/main/resources
│       └── log4j2.xml (optional)
└── SearchEngineTest (project-tests)
    |── pom.xml (should not need modification)
    ├── src/test/java/edu/usfca/cs272
    │   ├── Project1Test.java
    │   └── (other test files here)
    ├── expected
    │   ├── index
    │   │   └── (expected index-*.json files)
    │   └── (other directories for future projects)
    ├── input
    │   ├── text
    │   │   └── (text files to use as input)
    │   └── (other directories for future projects)
    └── actual
        └── (output files generated by your code)
```

If you run a test from the **SearchEngineTest** project, the output files will appear in the **SearchEngineTest** project even though your code is in the **SearchEngine** project.

If you run the `main` method via a Runtime Configuration in Eclipse from the **SearchEngine** project, then your output files will appear in the **SearchEngine** project.
