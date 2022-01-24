---
layout: guides
navbar: Guides
title: Java and Eclipse Setup
key: 1

---

This guide will walkthrough the steps necessary to install the latest versions of Java and Eclipse on your local system.

## Install Java 16

You need to make sure you have the latest version of Java **Standard** Edition (SE) **Development** Kit **16** (JDK 16) installed on your system. When downloading, keep in mind:

  - Do NOT download Java 8, Java 11, or Java 15. We will be using Java 16 in class. There are some differences between Java 8, Java 11, Java 15, and Java 16, and the lecture code may not compile on your system.

  - Do NOT download Java Enterprise Edition (EE). We will be using the Standard Edition (SE) in class. Java EE is used to create enterprise applications.

  - Do NOT download just the Java Runtime Environment (JRE). The Java Development Kit (JDK) includes the JRE, which is necessary to run Java code. The JDK also includes the Java compiler, which we will need in class.

To install the Java SE 16 JDK, go to:

<https://www.oracle.com/java/technologies/javase-jdk16-downloads.html>

Download the appropriate file for your system. Run the installer and follow the prompts.

![Java Installer]({{ "/images/java-installer.png" | relative_url }}){: .is-400 }

Once done, open a terminal window and verify the version using `java -version` and `javac -version`. The output will be similar to:

```shell
% java --version
java 16.0.2 2021-07-20
Java(TM) SE Runtime Environment (build 16.0.2+7-67)
Java HotSpot(TM) 64-Bit Server VM (build 16.0.2+7-67, mixed mode, sharing)
```

```shell
% javac --version
javac 16.0.2
```

Note that `%` above indicates the command prompt, and the lines below that are the output.

If when you verify the version of `java` and `javac`, it does not default to your new installation, then you might need to do some extra setup in Eclipse. See the "Verify Eclipse Java Settings" section below.

<i class="fas fa-info-circle"></i>
Java [removed auto-update capability](https://www.oracle.com/technetwork/java/javase/11-relnote-issues-5012449.html#Important_Changes) for Windows and MacOS systems. You will need to manually check when new versions of Java 16 are released.
{: .notification }

## Setup Folders (Optional)

I recommend you create a `CS 272` or `cs272` folder, and within it create these subfolders:

  - `Workspace`: This will be the folder for your Eclipse workspace.

  - `Repositories`: This will be the folder for your GitHub repositories that will be used for homework and project submission (and Eclipse).

    You can configure Eclipse to always save your CS 272 code in this folder in the "Version Control (Team) » Git" settings:

    ![Git Settings]({{ "/images/eclipse-version-control-git.png" | relative_url }}){: .is-600 }

Eclipse does not behave well when you combine or nest the `Workspace` and `Repositories` folders. **Keep these separate!**

## Install Eclipse

![About Eclipse]({{ "/images/eclipse-about.png" | relative_url }}){: .is-400 }

You need to make sure you have the latest **Eclipse IDE for Java Developers** package for **Eclipse 2021-06**. The direct download link is:

<https://www.eclipse.org/downloads/packages/release/2021-06/r/eclipse-ide-java-developers>

Do NOT download the IDE for Java EE Developers, as we are using Java SE in class. There are installers available for Windows, Mac OSX, and Linux. Once downloaded, double-click the installer.

<i class="fas fa-info-circle"></i>
Mac Users: I recommend you move the Eclipse.app file into your "Applications" folder for easy access.
{: .notification }

## Verify Eclipse Java Settings

If you installed the latest version of Java before Eclipse, Eclipse will usually use that version of Java automatically. Otherwise, you may need to change the Java settings within Eclipse.

The first step is to make sure Eclipse is aware of your new Java installation. Open the Eclipse preferences and go to the "Java" » "Installed JREs" settings:

![Eclipse Screenshot]({{ "/images/eclipse-installed-jres.png" | relative_url }}){: .is-400 }

If you do not see your newly installed version of Java, click the "Search" button to tell Eclipse where to find it. Then, I recommend removing any other installations from this window.

The next step is to configure Eclipse to use this version when **running** Java code. Open the "Java" » "Installed JREs" » "Execution Environments" panel:

![Eclipse Screenshot]({{ "/images/eclipse-execution-environments.png" | relative_url }}){: .is-400 }

Click on "JavaSE-16" and make sure your newest installation is selected. If you do not see "JavaSE-16" listed, you need to update your version of Eclipse.

After that, the final step is to configure Eclipse to use this version when **compiling** Java code. Go to the "Java" » "Compiler" settings in the Eclipse preferences:

![Eclipse Screenshot]({{ "/images/eclipse-java-compiler.png" | relative_url }}){: .is-400 }

Make sure `16` is selected from the dropdown menu. Make sure to apply those changes!
