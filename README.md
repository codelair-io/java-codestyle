# codelair.io CheckStyle-package

This is our checkstyle-package intended to be used in Maven projects. The checks are not quite as strict as Sun's original because those
were designed in a time before CDI, EJB, et cetera. Also, some default checkstyle checks also cause unnecessary frustration without
necessarily aiding readability. But don't be fooled, this package still makes your life difficult if you're a sloppy coder ;).

## Usage

In your Maven project, add:

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-checkstyle-plugin</artifactId>
  <version>3.0.0</version>
  <executions>
    <execution>
      <goals>
        <goal>check</goal>
      </goals>
    </execution>
  </executions>
  <dependencies>
    <dependency>
      <groupId>io.codelair.quality</groupId>
      <artifactId>checkstyle</artifactId>
      <version>RELEASE</version>
    </dependency>
  </dependencies>
</plugin>
```

This will by default use the `sun_checks.xml` (which really is a copy of `codelair_library_checks.xml`). If you want to use the checks
which do not enforce Javadoc, also following config-section to the plugin:

```xml
<configuration>
  <configLocation>codelair_checks.xml</configLocation>
</configuration>
```

## Which checkstyle-configuration to use

* *sun_checks* is the *maven-checkstyle-plugin*-default. In this package it's really just a copy of *codelair_library_checks* and we have it, because forgetting to set the `configLocation` would mean checkstyle uses the original *sun_checks*.
* *codelair_library_checks* is the default checkstyle-config which enforces most things (including Javadoc)
* *codelair_checks* is the same as above except that it only validates Javadoc, if present.

### Overview of checks

* No tabs (if you have happen to work at Pied Piper this probably makes this checkstyle package a no-go for you).
* Ignores Java 11 *module-info.java*.
* *final* is a good thing.
* whitespace between parameters, operators et cetera.
* (if appropriate config is used) enforces javadoc on public methods, classes, et cetera.
* Files should end with a new-line.
* Don't hide members.
* Empty-blocks are allowed only if there is a comment.
* Empty catch is only allowed if exception variable is called *ignored*.
* Curly-brackets start at the end of a line and end on a new-line.
* For clarity, operators start must be on a newline, if they are part of a multiline-statement.
* Meaningless blocks are not allowed (i.e. blocks that are not preceded by if/while/for...).
* if/while/... must have curly-brackets even if they are just one line.
* Variables, Method-names, constants, class-names, package-names must adhere to common Java-rules (camel-case, et cetera).
* modifier-ordering should follow sun-conventions (private static final, not private final static).
* No switch without default.
* No trailing white-space.
* No *-imports.
* No imports to JVM-internal classes.
* Magic-numbers must be constants.
* Equals comes with hashCode.
* Overly long boolean-statements are not allowed.
* Disallow redundant modifiers.
* Unused imports are not allowed.
* Lines should not be wider than 140 characters.
* Files should not be longer than 2000 lines.
* And a couple of others (bunch of white-space rules et cetera)...

## TODO

* Use Maven-resource-filtering magic so we don't have to duplicate similar files (sun_checks is the same as codelair_library_checks and codelair_checks is identical except the Javadoc-validation).
