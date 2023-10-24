# Introduction to Gradle

## Introduction

When creating Java applications, there can be a lot of additional complexity and overhead beyond simply writing Java code. Although we'd like to focus our effort on the codebase of our project, we still need to consider things such as building our project, installing and managing libraries, testing, and sharing our project with coworkers. While we could meticulously handle these tasks, using an application manager to perform them can be much easier. The application manager we use in this course is Gradle. In this lesson, we will discuss how Gradle can help you save time and effort with your projects, and you will learn to create a project using Gradle.

### Applying this in the job

Gradle streamlines the process of building your project. Without Gradle, you need to compile all your Java files manaually and make sure any third-party Java files are included. Gradle can perform this compiling process seemlessly, as well as run the program and even run the tests. Additionally, Gradle manages your **dependencies** for you. These resources are often called **libraries**. It's important to distinguish between a library and a dependency since the two are related and often used interchangably. A library is a group of code that performs an set of actions. A dependency is any library that your code needs to run ("my project _dependes_ on the Apache _library_"). Nearly every project you encounter will rely on dependencies your code will need to download and install. These tasks can be tedious and tiresome if done manually, but Gradle can gracefully build, test, run, and import dependencies into your project.

Not only can Gradle streamline compiling and running your project, but Gradle can also configure _how_ your project is built so other developers can build it the same way as you. Gradle uses a single configuration file called a **build script**. The build script ensures the project is set up the same way every time - with all the correct dependencies and build specifications. When working on a team of multiple developers, it's essential that everyone is building the project with the same configuration. Without Gradle and the build script, each team member would probably configure their projects differently, causing each project to behave differently. 

### Prerequisite knowledge

At this point, you should have some knowledge of writing simple scripts in Java and be comfortable using your command line (or terminal) to navigate file directories and install packages.

You may have used Gradle before in a previous project; however, no prior knowledge of Gradle or how it works will be necessary.

## Building a project without Gradle

Before we use Gradle, let's take a quick look at what it takes to run a Java project _without_ Gradle. Undertanding how Java compiles code can help you understand how Gradle works as well as appreciate its benefits. 

### How to build it

For this coding example, create a folder on your computer named `hello-world` using the command line. Mimic the following folder structure by adding a `srs/main/java` directory structure. Open `hello-world/src/main/java` in any text editor (such as Atom or VSCode) and create a new file named `Greeter.java`.

Your file structure should look like this:

```
hello-world
└── src
    └── main
        └── java
            └── Greeter.java

```

Copy the following code so that our `Greeter.java` file defines a Greeter class:

```java
public class Greeter {
  public static void main(String[] args) {
    greetUser("BloomtechStudent");
  }

  public static void greetUser(String username) {
    System.out.println("Hello " + username + "! Welcome to the server!");
  }
}
```

We can't run this java file just yet. We first need to convert it into a .class binary file. Then we can use the Java Virtual Machine (JVM) from our command line to run the program.

In your command line, navigate to `hello-world/src/main/java` where our `Greeter.java` file lives. Enter the following command to compile this file into a `Greeter.class` binary file.

```
javac Greeter.java
```

`javac` stands for “Java Compile” and it takes java files and turns them into class files that the computer can run. With our newly created class file, we can run our Java code with the following command:
```
java Greeter
```

You should see that it outputs: `Hello BloomtechStudent! Welcome to the server!`

You did it! Since this project doesn't use Gradle, we would need to repeat this process for each new Java file, and any time we changed our program. If we were using any dependencies, we'd have to manually download and do extra work to make sure those compiled as well. If you image this process in a project with 100's of Java files, you can start to see this doesn't scale well. It can become a dizzying task trying to build a large project.

Hopefully, you can start to appreciate how much nicer it'd be if we had this process automated for us. This is what an application manager such as Gradle can provide.

## Creating a Gradle project

In this section, we will create a similar application to the one above, this time using Gradle to manage the building of our project. Additionally, we will add a dependency and see how Gradle manages our dependencies. Being able to create and build a project using Gradle will allow you to automate more build processes in your own projects, potentially saving hours of work for yourself and your teammates. 

### How to build it

We will be using Gradle version 7.0.2. You can follow the tutorial on [this page](https://gradle.org/install/) for instructions specific to your operating system. Replace the listed version number with 7.0.2 to be consistent with our projects.

From your command line and with [Gradle installed](https://gradle.org/install/), create a new project folder named `intro-to-gradle`. Go into this folder and run the following command:

```
gradle init
```

You’ll be prompted first for the type of project, select `1` for `basic`. 

```
Select type of project to generate:
  1: basic
  2: application
  3: library
  4: Gradle plugin
Enter selection (default: basic) [1..4] 1
```

Next, you will be asked which build script language you will use. In this course, we will uae `Groovy` for all of our build scripts. With Groovy, we’ll only be using simple commands so there’s no need to learn it in-depth as we’ve done for Java. 

```
Select build script DSL:
  1: Groovy
  2: Kotlin
Enter selection (default: Groovy) [1..2] 1
```

Finally, you will be prompted for a project name, with the directory's name as the default option. You can pass in any empty character (just press enter/return) to use the default name.

After finishing the prompts, your complete command history should look something like this:

```
gradle init

Select type of project to generate:
  1: basic
  2: application
  3: library
  4: Gradle plugin
Enter selection (default: basic) [1..4] 1

Select build script DSL:
  1: Groovy
  2: Kotlin
Enter selection (default: Groovy) [1..2] 1

Project name (default: intro-to-gradle):

> Task :init
Get more help with your project: Learn more about Gradle by exploring our samples at https://docs.gradle.org/7.0.2/samples

BUILD SUCCESSFUL in 4s
2 actionable tasks: 2 executed
```

You should now see that your directory contains several new files and folders:

```
build.gradle
gradle		
gradlew		
gradlew.bat
settings.gradle
```

The `build.gradle` file is where we can configure how Gradle builds and runs your project. Open `build.gradle` in a text editor and add the Java and application plugins by writing the following command:

```
plugins {
    id 'java'
    id 'application'
}
```

These lines tell Gradle to add certain build commands to this project. If you run `gradle tasks`, you should see a long list of tasks that Gradle can perform for you. The most important commands are `build` and `run`, but we first need to add some code to our project, so let's do that next.

We'll want to add our code under the directory `src/main/java` since that's where Gradle will look for it by default. Create the same `src/main/java` file structure we did before. Within the `java` folder, add the `Greeter.java` file we used in the previous example. The project’s file structure should look like this:

```
├── build
├── build.gradle
├── gradle
├── gradlew
├── gradlew.bat
├── settings.gradle
└── src
    └── main
        └── java
            └── Greeter.java
```
You can now run the project using `gradle run`, but you will see an error with the message: `No main class specified and classpath is not an executable jar.` This means we need to specify in our build script the class which contains the entry point for our application. Of course, we only have one class, and we can specify this in `build.gradle` by adding the following script:

```
application {
   mainClass = 'Greeter'
}
```

We added a block of code called `application`. We added `application` as a plugin to the build script, and one of the commands the `application` added was `run`. This block configures the `application` plugin by telling it where the main class is located. 

Run the project again by entering `gradle run` into the terminal. You should see now that it outputs the message to the console.

```
Hello BloomtechStudent! Welcome to the server!
```

Anytime you change code, all you will need to run is `gradle run`. No need to compile the code first and then run it. It's all done for you in one line. Time saved!

## Using our dependency in our code

Currently, we have a Greeter application that uses a `greetUser` method to welcome a user to the (pretend) server. Let's say we want to validate that usernames contain only alphanumeric characters. There's a library for that! It's called the Apache Commons lang3 library. Manually bringing in a dependency can require a lot of steps, but Gradle makes it easy. We only need to tell Gradle where to find it.

### How to build it

We'll first need to specify where the library is hosted. Many hosting networks exist that house many popular libraries and we need to specify which hosts Gradle should look at to search for libraries. The host that we’ll use is `mavenCentral`, which is one of the most popular hosting networks. 

In our build script we first add `mavenCentral` to our list of repositories like so:

```
repositories {
    mavenCentral()
}
```

With the repository listed, we can now add our Apache Commons dependency. A quick Google search for “StringUtils gradle dependency” will usually lead you to the line you need to add. Doing this we can find the library on [Maven Repository's site](https://mvnrepository.com/artifact/org.apache.commons/commons-lang3/3.0) and we can copy the provided Groovy instruction.

```
dependencies {
    implementation 'org.apache.commons:commons-lang3:3.0'
}
```

With the dependency in place, run `gradle build` and after a successful build, the Apache Commons lang3 library is now available in your project. Notice that we did not run the `gradle run` command. That's because running `gradle build` will get those dependencies for us without running the project, saving us some time. 

In our Greeter class, we want to check that our username only contains alphanumeric values. Let’s add this check inside the `greetUser` method by using our new dependency’s `StringUtils` class to validate our usernames:

```java
public static void greetUser(String username) {
    if (StringUtils.isAlphanumeric(username)) {
        System.out.println("Hello " + username + "! Welcome to the server!");
    } else {
        throw new RuntimeException("Invalid username!");
    }
}
```

Your IDE will likely import `StringUtils`, but in case it doesn’t, add this line to the top of your file:

```
import org.apache.commons.lang3.StringUtils;
```

In the `main` method of the `Greeter` class, add another `greetUser` call with the invalid user `"Bloom_Admin@email.com"`:

```java
public static void main(String[] args) {
  greetUser("BloomtechStudent");
  greetUser("Bloom_Admin@email.com");
}
```

Now we can run `gradle run` and run the jar file.
*Note: `gradle run` is what happens when you press the green arrow in IntelliJ*

You should see we get an exception for `"Bloom_Admin@email.com"` and that it greets `"BloomtechStudent"`.

Expected Output:
```
Hello Bloomtech! Welcome to the server!
Exception in thread "main" java.lang.RuntimeException: Invalid username!
	at Greeter.greetUser(Greeter.java:13)
	at Greeter.main(Greeter.java:6)
```

If you got the error message, you're code is working with the new dependency as exepcted.

## Conclusion

We've now seen how an application manager like Gradle can simplify the process of building our Java projects. Gradle is something you will see here and throughout your career, so it's good to be familiar with how it works, especially when it comes to adding dependencies.  Gradle can do so much more, but for now, you have enough knowledge to move on. 






