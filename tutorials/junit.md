<frontmatter>
  title: "Using JUnit"
  pageNav: 2
</frontmatter>

# Using JUnit

<div class="lead">

[JUnit](https://junit.org/junit5/) is a testing framework for Java.
</div>

<div id="junit-use-gradle">

As JUnit is a third-party library, you need to add support to it specifically in your project. Given below is how you can do that using the <tooltip content="a build tool and a dependency management tool">Gradle</tooltip>. While it is possible to add JUnit to your project without Gradle, **we strongly recommend using Gradle** as it can make things easier in the long run.<br>
If you have not done that yet, follow the [_Gradle Tutorial_](gradle.html) to add Gradle support to the project first.
</div>

This tutorial explains how to use JUnit in a project, _with Gradle_.

<!-- ======================================================== -->


<div id="junit-conventions">

## Conventions to Follow

Here are the conventions to follow, when using JUnit in a Gradle project:

1. Add test code in a folder named `[project root]\src\test\java\` folder.
1. Name the test class to match the class being tested (`Todo.java` can be tested by `TodoTest.java`), and put it in a package to match %%(reason: if packages are matched, the test class can access package-private members of the target class)%%.<br>
   For example,
   * Class being tested `seedu.duke.Todo`: `src\main\java\seedu\duke\Todo.java`
   * Test class `seedu.duke.TodoTest`: `src\test\java\seedu\duke\TodoTest.java`

<div class="indented-level2">

<tree>
:far-folder: [project root] %%e.g., C:\courses\project\\%%
  :far-folder: src\
    :far-folder: ==main==\
      :far-folder: java\
        :far-folder: seedu\
          :far-folder: duke\
            :far-file: ==ToDo==.java
    :far-folder: ==test==\
      :far-folder: java\
        :far-folder: seedu\
          :far-folder: duke\
            :far-file: ==ToDoTest==.java
</tree>
<br>
</div>
</div>

<!-- ======================================================== -->


<div id="add-junit-to-gradle">

<box type="info" seamless>

### Quick pre‑checks (highly recommended)

1. **Project SDK**: In IntelliJ, go to **File → Project Structure → Project**.  
   - Set **Project SDK** to a valid JDK (e.g., Temurin/Oracle 17).  
   - Set **Language level** to match your JDK.
2. **Folder layout**: Ensure your code is in `src/main/java/...` and tests are in `src/test/java/...`.  
   - If you created a custom folder, right‑click it → **Mark Directory as → Test Sources Root**.
3. **Package mirroring**: Keep test packages the same as the main packages so package‑private members are accessible during testing.
</box>


<div id="add-junit-to-gradle">

## Configuring Gradle for JUnit

Add JUnit 5 (Jupiter) to your **Gradle** project with the minimal, copy‑pasteable setup below.  
This is all you need to compile and run JUnit tests.

**Minimum `build.gradle` (Groovy)**

```groovy {heading="build.gradle"}
plugins {
  id 'java'
}

repositories {
  mavenCentral()
}

dependencies {
  // JUnit 5 (Jupiter) API + engine (single artifact)
  testImplementation 'org.junit.jupiter:junit-jupiter:5.10.0'
}

test {
  // Tell Gradle to run JUnit 5 tests
  useJUnitPlatform()
}
```

<box type="tip" seamless> After editing <code>build.gradle</code>, open the 
**Gradle** tool window and click  **Reload All Gradle Projects** (or restart IntelliJ) so the IDE picks up the changes. </box> <panel header="Optional: more verbose test output" peek no-close no-switch> You can add this inside the <code>test { ... }</code> block to see passed/failed/skipped events and full stack traces:

```groovy
testLogging {
  events "passed", "skipped", "failed"
  exceptionFormat "full"
  showExceptions true
  showCauses true
  showStackTraces true
}
```

</panel> <panel header="Using Kotlin DSL? (build.gradle.kts)" peek no-close no-switch> Equivalent Kotlin DSL:
```kotlin
plugins {
  java
}

repositories {
  mavenCentral()
}

dependencies {
  testImplementation("org.junit.jupiter:junit-jupiter:5.10.0")
}

tasks.test {
  useJUnitPlatform()
}

```
</panel> </div> 

<!-- ======================================================== -->

<div id="first-unit-test">

## Writing the First JUnit Test

**Add a test class**, while following [the conventions given earlier in this page](#conventions-to-follow). If you don't follow those conventions, Gradle will not be able to find your test class. For example, if you have a class `src\main\java\seedu\duke\Todo.java`, you can add a test class `src\`==test==`\java\seedu\duke\`==TodoTest.java==. Here's some sample code:

```java{.line-numbers highlight-lines="8,13", heading="src\test\java\seedu\duke\TodoTest.java"}
package seedu.duke;  //same package as the class being tested

import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.assertEquals;

public class DukeTest {
    @Test
    public void dummyTest(){
        assertEquals(2, 2);
    }

    @Test
    public void anotherDummyTest(){
        assertEquals(4, 4);
    }
}
```

</div>

**Run tests**, either using the Intellij UI (preferred -- this makes debugging failed test cases easier) or using Gradle itself, as explained in the section below.

<!-- ======================================================== -->

## Running Tests

{% set play_button = '<span class="text-success">:fas-play:</span>' %}

****In Intellij IDEA:****

* To run a specific JUnit test class (e.g., `src/test/java/seedu/DukeTest.java`), right-click on the test class, and choose {{ play_button }} `Run {classname}`.

<box type="tip" seamless>

If tests don’t run or get “No tests found”, check **File → Settings → Build, Execution, Deployment → Gradle → Run tests using**:

- **Gradle** (recommended if your project builds with Gradle and uses Gradle tasks in CI), or  
- **IntelliJ IDEA** (can be simpler for debugging on small projects).

Switch if one runner can’t discover tests. Then **Reload All Gradle Projects**.

<panel header="Expand to see screenshot ..." peek no-close no-switch>
![Change IntelliJ settings to not use Gradle](images/gradle/intellijRunTestsUsingIntellij.png)
</panel>
</box>


* To run all tests in a folder (e.g., `src/test/java` folder), right-click on the folder, and choose {{ play_button }} `Run Tests in '...'`.
* Other supported IDEs (e.g., Eclipse, NetBeans, VS Code, etc.) have similar mechanisms.

****Using Gradle:****

* To run all tests in the project, run the Gradle task `test` ([more info on running Gradle tasks](gradle.md#running-gradle-tasks))
* [If using Intellij UI to run the `test` task] The location of the `test` task in the Gradle task hierarchy is `Tasks -> verification -> test` (see screenshot below).<br>
    <pic src="images/junit/gradleTaskHierarchy.png" />

<div id="other-ways-of-running-tests">

****Other ways:****

* There is also [a way to run JUnit tests in the console (without Gradle or an IDE)](https://junit.org/junit5/docs/current/user-guide/#running-tests-console-launcher), which is not used as much as the above two methods.

</div>

<!-- ======================================================== -->

<div id="useful-test-cases">

## Writing Useful JUnit Tests

After you are able to run JUnit tests successfully using a dummy test class such as the above, you can add more tests and test classes as necessary.

To learn how to write useful JUnit test cases, refer [this section](https://se-education.org/se-book/cppToJava/junit/basic/index.html) of our SE book. For a quick overview of more advance JUnit features, refer [this section](https://se-education.org/se-book/cppToJava/junit/intermediate/index.html).

</div>

<!-- ======================================================== -->

## Resources

* [JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/)
* [Gradle documentation for JUnit](https://docs.gradle.org/current/userguide/java_testing.html#using_junit5)
