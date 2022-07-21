# Multi-Schema Validator Toolkit

The core component of this toolkit is the Multi-Schema XML Validator (MSV). It is a Java technology tool to validate XML documents against several kinds of XML schemata. It supports RELAX NG, RELAX Namespace, RELAX Core, TREX, XML DTDs, and a subset of XML Schema Part 1.
<br/>
Most outstanding is the design of MSV core using the [Abstract grammar model (AGM)](https://xmlark.github.io/msv/nativeAPI.html). This is a schema-independent grammar model. All supported schemata are parsed into this internal representation. This model, coupled with the grammar reader, may be useful for other applications. For instance, two use cases are the generation of source code using [schema2template](https://tdf.github.io/odftoolkit/generator/index.html) or the [ODF Validator](https://tdf.github.io/odftoolkit/conformance/ODFValidator.html).
<br/>The builds of all MSV sub-projects were tested sucessfully using JDK 8, JDK 11 and JDK 17 on Windows and Linux.

## Installation

All subprojects are are available from
[Maven Central](https://search.maven.org/search?q=g:net.java.dev.msv).
For instance, Using MSV core as dependency in your Maven project via

    <dependency>
      <groupId>net.java.dev.msv</groupId>
      <artifactId>msv-core</artifactId>
      <version>2011.01</version>
    </dependency>

## Usage

MSV's documentation is stored in the `main` branch and is
available online at
[https://xmlark.github.io/msv](https://xmlark.github.io/msv)


## Contributing

You have three options if you have a feature request, found a bug or
simply have a question about System Rules.

* [Write an issue.](https://github.com/xmlark/msv/issues/new)
* Create a pull request. (See [Understanding the GitHub Flow](https://guides.github.com/introduction/flow/index.html))
* [Write a mail to our mailing list (while list in progress to me)](mailto:svanteschubert@apache.org)

## Development Guide

The original detailed MSV development documentation can be found [at our GitHub pages](https://xmlark.github.io/msv/).</br>

MSV is build with [Maven](http://maven.apache.org/). If you
want to contribute code than

* Please write a test for your change.
* Ensure that you didn't break the build by running `mvn test`.
* Fork the repo and create a pull request. (See [Understanding the GitHub Flow](https://guides.github.com/introduction/flow/index.html))

The basic coding style is described in the
[EditorConfig](http://editorconfig.org/) file `.editorconfig`.

## Directory structure

MSV consists of a number of sub-projects. Each sub-projects has its own directory, its own build script, etc.

| sub-project       | description                                                                                                                                |
|:------------------|:-------------------------------------------------------------------------------------------------------------------------------------------|
| **xsdlib**        | **XML Schema Datatype (XSD) Library**<br/>An implementation of W3C XML Schema Part 2 [(see JavaDoc)](https://xmlark.github.io/msv/api/xsdlib/index.html). |
| testharness       | **Test harness**<br/>Used to parse composite test suite files (.ssuite).                                                                   |
| **[msv core](./msv/README.md)**      | **[Multi-Schema XML Validator](./msv/README.md)**<br/>A schema model and validator implementation [(see JavaDoc)](https://xmlark.github.io/msv/api/msv/index.html).</br>Dependent on XSDLib and testharness.                       |
| **generator**     | **XML Instance Generator** A tool that produces valid XML documents by reading a schema. Dependent on MSV.                                 |
| schmit            | **MSV Schmit (Schema-in-transformation XSLT add-on)**<br/>XSLT Extension For Schema Annotation.                                            |
| relames           | **Multi-Schema XML Validator Schematron add-on**<br/>An experimental implementation of RELAX NG + Schematron validation. Dependent on MSV. |
| **rngconverter**  | **RELAX NG Converter**<br/>reads a schema and produces an equivalent RELAX NG schema. Dependent on MSV.                                    |
| tahiti            | **Data-binding implementation**                                                                                                            |
| trexconverter     | **TREX Converter**<br/>Reads a schema and produces an equivalent TREX pattern.                                                             |

***NOTE:*** Not [all previous forks and releases](https://github.com/svanteschubert/msv-merge-project) embrace all the projects below, only the latest msv does.

## MSV Copyright
The sources of the deliverables of the sub-projects in bold (in the table above) have a [BSD license](https://en.wikipedia.org/wiki/BSD_licenses). but their tests and all other sources have missing licing headers.
Sometimes Apache 1.1 licence header do exist. 
The original MSV code repository from Sun/Oracle is no longer accessible. The Glassfish team as new owner is not responding [https://javaee.github.io/other-migrated-projects.html](https://javaee.github.io/other-migrated-projects.html) but [a fork exists from the former Code Owner Kohsuke Kawaguchi (KK) at Oracle](https://github.com/kohsuke/msv).

* KK's fork embraces the Maven releases from 2010 to 2011.
* The Maven release 2011 by RedHat is identical to the one 2011 on Maven central adding Generic Java Types and the default attribute value feature.
* Oracle did several releases 2013. They fixed the copyright header for the deliverables of the sub project in bold above. The sources are [taken from the source JAR of the Maven Central repository](https://github.com/svanteschubert/msv-merge-project).
* KK's fork is at the moment being located and maintained on branches at [https://github.com/xmlark/msv/](https://github.com/xmlark/msv/).


### There are several other directories which are used to store other materials.
| directory | description |
| :-------- | :---------- |
| docs | Project documentation. Files in this directory are shown at [https://xmlark.github.io/msv/](https://xmlark.github.io/msv/). |

### Sub-project structure
Most of the sub-projects have a similar directory structure aligned to [the standard directory layout of the Maven build system](https://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html).

| directory | description |
|:----------| :---------- |
| src/main  | keeps source files. Files in this directory will be included in the release package. |
| src/test  | keeps test files. Files in this directory will NOT be included in the release package. JUnit is used throughout the project, and every test code must have "Test.java" as suffix to be recognized as a test. |
| target    | keeps the compiled .class files. both "test" and "src" are compiled into this directory. |


## Build instruction
To build the entire project, use [Maven 3](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html).</br> [Maven is downloadable for free at Apache.](https://maven.apache.org/download.cgi).
To build via command line at project root level use:
'***mvn install***'
This builds the release packages for all sub-projects in a proper order.
When preparing release packages, it is a good idea to use this target so that dependencies are processed correctly. (But you should run a project-local "release" first to make sure that there is no error in the repository.)

### Project-wise build
When you are working on a sub-project, you can build in the sub-project directory via '***mvn install***' saving some time by building this alone.
