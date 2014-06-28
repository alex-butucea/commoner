# Commoner
A collection of generic Phing targets for PHP projects.

## Usage
Install via Composer and include commoner.xml in your Phing build file to inherit the following targets:

- `build` - Execute full build process
- `clean` - Cleanup build artifacts
- `generate` - Execute all generation targets:
    - `generate-coverage-report` - Generate code coverage report
    - `generate-phpdoc` - Generate ApiGen PHP Docs
    - `generate-phplint-report` - Generate PHP Lint report
    - `generate-standards-report` - Generate PSR-2 code standards report
- `prepare` - Execute all preparation tasks:
    - `prepare-build-dir` - Prepare build output dir
    - `prepare-autoloader` - Prepare autoloader
    - `prepare-coverage-report` - Setup test coverage db
- `test` - Execute all framework tests
- `test-specific` - Execute specific framework test

Be sure to define a `basedir` property within your project build file to ensure paths are resolved correctly.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project name="foo" basedir="." default="build">
    <import file="${project.basedir}/vendor/alex-butucea/commoner/commoner.xml"/>
</project>
```

## Customisation
Paths and options used by the above targets can be overridden by defining the following properties in your build.xml:

- `vendor-dir` - Path to composer-downloaded dependencies
- `source-dir` - Your project source code location
- `tests-dir` - Where your unit tests live
- `build-dir` - Generated Phing output goes here
- `apigen-dir` - ApiGen project path
- `doc-dir` - Where generated documentation goes
- `standards-report-dir` - PSR-2 standards report will go here
- `phplint-report-dir` - Generated PHPLint report goes here
- `test-log-dir` - Where the PHPUnit test log will be output
- `test-report-dir` - PHPUnit test report will be saved here
- `coverage-report-dir` - Generated PHPUnit code coverage report will go here
- `coverage-report-styles-dir` - Where code coverage report styles live

Filenames available for customisation:

- `autoload-file` - File name of composer-generated autoloader
- `apigen-file` - Name of ApiGen executable
- `standards-report-file` - File name of generated PSR-2 standards report
- `phplint-report-file` - What the PHPLint report will be called
- `test-bootstrap` - Name of test bootstrap file
- `test-log-file` - What PHPUnit test log will be called
- `coverage-report-db` - File name of code coverage report database
- `coverage-report-file` - Code coverage report file name

Below is a snippet from the Commoner build file with above properties and their default values:

```xml
<!-- ============================================  -->
<!-- Directories used by dependent targets         -->
<!-- ============================================  -->
<property name="vendor-dir"                 value="${project.basedir}/vendor"/>
<property name="source-dir"                 value="${project.basedir}/src"/>
<property name="tests-dir"                  value="${project.basedir}/tests"/>
<property name="build-dir"                  value="${project.basedir}/build"/>
<property name="apigen-dir"                 value="${vendor-dir}/apigen/apigen"/>
<property name="doc-dir"                    value="${build-dir}/doc"/>
<property name="standards-report-dir"       value="${build-dir}/standards-report"/>
<property name="phplint-report-dir"         value="${build-dir}/phplint-report"/>
<property name="test-log-dir"               value="${build-dir}/test-log"/>
<property name="test-report-dir"            value="${build-dir}/test-report"/>
<property name="coverage-report-dir"        value="${build-dir}/coverage-report"/>
<property name="coverage-report-styles-dir" value="${vendor-dir}/phing/phing/etc"/>

<!-- ============================================  -->
<!-- Filenames used by dependent targets           -->
<!-- ============================================  -->
<property name="autoload-file"         value="autoload.php"/>
<property name="apigen-file"           value="apigen.php"/>
<property name="standards-report-file" value="standards"/>
<property name="phplint-report-file"   value="phplint"/>
<property name="test-bootstrap"        value="bootstrap.php"/>
<property name="test-log-file"         value="tests.xml"/>
<property name="coverage-report-db"    value="database"/>
<property name="coverage-report-file"  value="coverage.xml"/>
```

## Prerequisites
- Composer
- PHP 5.3.3+
- Xdebug 2.0.5+
- XSL

---------------------------------------------------
Copyright (c) 2013 Alex Butucea <alex826@gmail.com>
