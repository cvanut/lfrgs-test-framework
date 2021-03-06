# LFRGS Test Framework

## TO USE

- clone repo
- get the jar or the module
	- jar
		- run gradle build on test-api modules
		- copy jars into your module; adding them as part of your bnd
	- module
		- copy module src into your liferay workspace project
		- fix any dependencies in build.gradle files
		- reference the test-api modules in your own module
- for selenium
	- implement your own JUnit test classes that specify either the **LiferaySeleniumTestRunner** or **LiferaySeleniumSuiteRunner**
	- **WebDriverField** and **@Browsers** annotations are available
- for cucumber
	- write a feature file following the normal gherkin syntax [see here](/master/modules/dummy/dummy-portlet/src/test/resources/feature/DummyPortlet.feature) for an example
	- implement a *FeatureRunner* using the provided Cucumber and Framework annotations [see here](/modules/dummy/dummy-portlet/src/test/java/com/liferay/gs/test/dummy/functional/cucumber/DummyPortletFeatureRunner.java) for an example
	- write extensions of **WebDriverComponent** that define user interactions with the browser via the selenium webDriver
	- write extensions of **BaseStep** that use the **WebDriverComponents** to accomplish a complete user action This is what your feature file will reference [see here](/modules/dummy/dummy-portlet/src/test/java/com/liferay/gs/test/dummy/functional/cucumber/step/ButtonSteps.java) for an example

## Overview

This test framework is intended to provide testing api that can be used to create tests quickly and easily. The Goal is to allow developers simple extension points to be able to write functional, integration, and unit tests.

This project is created with the Liferay Workspace. There are two module groups: **dummy** and **tests**

### Dummy module group

These modules provide sample code that simplistically represents what may be in a real project. These moduels are intended to consume the **tests** modules in order to create their own tests.

there are currently three modules:
- dummy-portlet: [liferay MVC portlet](/modules/dummy/dummy-portlet/README.md)
- dummy-service-builder-api: liferay service builder api module
- dummy-service-builder-service: liferay service builder implementation module

### Tests module group

Modules contained within the tests group are meant to be used in tests. These are the heart of the project and will ultimately be available to a developer as a gradle/maven dependency.

there are three sub-groups
- **functional**: used to demonstrate what the end user will do. no code is tested directly, only web elements and user actions
- **integration**: used to test how two or more pieces of code interact with one another. typically done through mocking the environment, or spinning up a test environment in order to test its various components. test the code directly.
- **unit**: used to test individual pieces of code, without any external interaction. All dependencies should be mocked. test the code directly.

these sub-groups represent the different kinds of tests that developers will need to write in order to fully cover their projects.

the modules contained within each sub-group provide api/extension points to make accomplishing those specific test tasks easier.

currently there are 5 modules. 4 functional test modules and 1 unit test module:
- functional
    - [cucumber-test-api](/modules/tests/functional/cucumber-test-api/README.md)
    - [cucumber-test-components](/modules/tests/functional/cucumber-test-components/README.md)
    - [selenium-test-actions](/modules/tests/functional/selenium-test-actions/README.md)
    - [selenium-test-api](/modules/tests/functional/selenium-test-api/README.md)
- unit
    - [proxy-test-api](/modules/tests/unit/proxy-test-api/README.md)