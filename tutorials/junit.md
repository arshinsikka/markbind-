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

**Add a class and a matching test**, while following [the conventions given earlier in this page](#conventions-to-follow).  
Here’s a minimal working example:

```java {heading="src/main/java/example/Calculator.java"}
package example;

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

```java
package example;

import org.junit.jupiter.api.*;

class CalculatorTest {

    Calculator c;

    @BeforeEach
    void setUp() {
        c = new Calculator();
    }

    @Test
    void add_twoNumbers_returnsSum() {
        Assertions.assertEquals(5, c.add(2, 3));
    }
}
```

**Run tests**, either using the Intellij UI (preferred -- this makes debugging failed test cases easier) or using Gradle itself, as explained in the section below.

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

<div id="debugging-tests">

## Debugging Tests (IntelliJ)

1. Open a test file and **click in the gutter** to set a breakpoint.
2. Click the **bug icon** (or right‑click the test/class → **Debug '…'**).
3. Use the debug toolbar to **Step Over (F8)**, **Step Into (F7)**, and **Resume (F9)**.
4. Hover variables to inspect values or use **Evaluate Expression** (`Alt/Option+F8`).

</div>

<!-- ======================================================== -->

<div id="test-coverage">

## Running with Coverage (IntelliJ)

1. Right‑click a test or class and choose **Run '…' with Coverage** (or use the gutter coverage icon).
2. Open the **Coverage** tool window to view line coverage and navigate to uncovered lines.

<pic src="images/junit/run-with-coverage.png" />
<pic src="images/junit/coverage-tool-window.png" />

<box type="info" seamless>
If you run via Gradle, HTML reports (when enabled) appear at  
`build/reports/tests/test/index.html`.
</box>

</div>


<!-- ======================================================== -->

<div id="useful-test-cases">

## Writing Useful JUnit Tests

After you are able to run JUnit tests successfully using a dummy test class such as the above, you can add more tests and test classes as necessary.

To learn how to write useful JUnit test cases, refer [this section](https://se-education.org/se-book/cppToJava/junit/basic/index.html) of our SE book. For a quick overview of more advance JUnit features, refer [this section](https://se-education.org/se-book/cppToJava/junit/intermediate/index.html).

</div>

<!-- ======================================================== -->

## Troubleshooting (quick fixes)

- **“No tests found”**  
  Ensure `test { useJUnitPlatform() }` is in `build.gradle`, test methods use JUnit 5 annotations (`@Test` from `org.junit.jupiter.api`), and your **Run tests using** setting matches your build (Gradle vs IntelliJ). Reimport Gradle.
- **“Cannot resolve symbol org.junit…”**  
  Add the JUnit dependency in `dependencies { testImplementation 'org.junit.jupiter:junit-jupiter:5.10.0' }` and reimport Gradle.
- **Tests run twice**  
  Disable either IDE delegation or Gradle test running (avoid mixed runners). Check **Build Tools → Gradle** and **Build Tools → Maven** settings if applicable.
- **Module not specified / Scope issues**  
  Edit the Run Configuration: pick **All Tests in <module>** or **Class/Package** as needed.



<!-- ======================================================== -->

## Resources

* [JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/)
* [Gradle documentation for JUnit](https://docs.gradle.org/current/userguide/java_testing.html#using_junit5)
