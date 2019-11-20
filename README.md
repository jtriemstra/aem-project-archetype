# AEM project archetype

[![CircleCI](https://circleci.com/gh/adobe/aem-project-archetype.svg?style=svg)](https://circleci.com/gh/adobe/aem-project-archetype)

![](https://raw.githubusercontent.com/wiki/adobe/aem-project-archetype/screenshots/archetype.png)

This archetype creates a minimal Adobe Experience Manager project as a starting point for your own projects. The properties that must be provided when using this archetype allow to name as desired all parts of this project.

See the [Getting Started with AEM Sites - WKND Tutorial](https://docs.adobe.com/content/help/en/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html) on the Adobe Help Center website for an example of how to use it.

This project has a number features that are intended to offer a convenient starting point for new projects:

* Language Master / Country structure
  * A language master structure and country top level page
  * Live copy of the top level page in the specified language
  * Blueprint

* Content and Experience fragment templates based on the editable template feature
  * Example content policy

* Page component
  * Based on the [AEM Sites Core Component page](https://github.com/adobe/aem-core-wcm-components/tree/master/content/src/content/jcr_root/apps/core/wcm/components/page/v2/page)
  * customfooterlibs.html and customheaderlibs.html snippet to load additional JS and CSS clientlibs according to the {cssId} property
* Content Components
  * Proxy components for all AEM Sites Core Components of the latest released version. For instance  accordion, carousel, text and much 
  more. For a complete overview see  [AEM Sites Core Components](https://github.com/adobe/aem-core-wcm-components)
  * Example: helloworld example of custom HTL component with SlingModels for the logic

* Frontend module
  * Build process based on Webpack with support for Sass and TypeScript / ES6
  * Automatic AEM ClientLib generation
  * CSS class names follow BEM naming conventions
  * Component-specific styles stored within each component

* Configurations
  * Device emulators displayed in the authoring interface
  * Allow direct drag & drop of assets from the content finder into layout container (6.3 TouchUI)
  * Dictionary structure for internationalizing hardcoded strings

* Bundle with some examples
  * Models: Models for more complex business logic of components
  * Servlets: Rendering the output of specific requests
  * Filters: Applied to the requests before dispatching to the servlet or script
  * Schedulers: Cron-job like tasks

* Tests
  * Unit tests
  * Integration tests
  * Client-side Hobbes tests within developer mode
  
  
## Provided Maven profiles
The generated maven project support different deployment profiles when running the Maven install goal `mvn install` within the reactor.

Id                        | Description
--------------------------|------------------------------
autoInstallBundle         | Install core bundle with the maven-sling-plugin to the felix console
autoInstallPackage        | Install the ui.content and ui.apps content package with the content-package-maven-plugin to the package manager to default author instance on localhost, port 4502. Hostname and port can be changed with the aem.host and aem.port user defined properties. 
autoInstallPackagePublish | Install the ui.content and ui.apps content package with the content-package-maven-plugin to the package manager to default publish instance on localhost, port 4503. Hostname and port can be changed with the aem.host and aem.port user defined properties.
autoInstallSinglePackage | Install the `all` content package with the content-package-maven-plugin to the package manager to default author instance on localhost, port 4502. Hostname and port can be changed with the aem.host and aem.port user defined properties. 
autoInstallSinglePackagePublish | Install the `all` content package with the content-package-maven-plugin to the package manager to default publish instance on localhost, port 4503. Hostname and port can be changed with the aem.host and aem.port user defined properties.

The profile `integrationTests` is also available for the verify goal, to run the provided integration tests on the AEM instance.  

## Usage

To use a released version of this archetype:

Either use the [AEM Eclipse extension](https://docs.adobe.com/docs/en/dev-tools/aem-eclipse.html) and follow the New Project wizard (choosing AEM Sample Multi-Module Project)...

Or use your mvn skills:

    mvn archetype:generate \
     -DarchetypeGroupId=com.adobe.granite.archetypes \
     -DarchetypeArtifactId=aem-project-archetype \
     -DarchetypeVersion=22

Where 22 is the archetype version number that you want to use (see archetype versions below).

**For Windows users**: In case you are getting `A required privilege is not held by the client.` error, you will need to run the archetype as an administrator or [setup rights for creating symbolic links](https://stackoverflow.com/questions/23217460/how-to-create-soft-symbolic-link-using-java-nio-files/24353758#24353758).

### Available properties

Name                        | Default | Description
----------------------------|---------|--------------------
groupId                     |         | Base Maven groupId
artifactId                  |         | Base Maven ArtifactId
version                     |         | Version
package                     |         | Java Source Package
appsFolderName              |         | /apps folder name
artifactName                |         | Maven Project Name
componentGroupName          |         | AEM component group name
contentFolderName           |         | /content folder name
confFolderName              |         | /conf folder name
cssId                       |         | prefix used in generated css
packageGroup                |         | Content Package Group name
siteName                    |         | AEM site name
optionAemVersion            |  6.5.0  | Target AEM version
language_country            |   en_us | language / country code to create the content structure from (e.g. en_us)
optionIncludeExamples       |    y    | Include a Component Library example site
optionIncludeErrorHandler   |    n    | Include a custom 404 response page
optionIncludeFrontendModule |    n    | Include a dedicated frontend module
isSingleCountryWebsite      |    y    | Create language-master structure in example content
optionDispatcherConfig      |   none  | Generate a dispatcher configuration module

Note: If the archetype is executed in interactive mode the first time properties with default values can't be changed (see 
[ARCHETYPE-308](https://issues.apache.org/jira/browse/ARCHETYPE-308) for more details). The value can be changed when the property 
confirmation at the end is denied and the questionnaire gets repeated, or by passing the parameter in the command line (e.g. 
`-DoptionIncludeExamples=n`).

### Requirements

The latest version of the archetype has the following requirements:

* Adobe Experience Manager 6.3.3.0 or higher
* Apache Maven (3.3.9 or newer)
* Adobe Public Maven Repository in maven settings, see [Knowledge Base](https://helpx.adobe.com/experience-manager/kb/SetUpTheAdobeMavenRepository.html) article for details.

For a list of supported AEM versions of previous archetype versions, see [historical supported AEM versions](VERSIONS.md).

## Building

To compile and use an edge, local version of this archetype:

    mvn clean install

Then change to the directory in which you want to create the project and run:

    mvn archetype:generate \
     -DarchetypeGroupId=com.adobe.granite.archetypes \
     -DarchetypeArtifactId=aem-project-archetype \
     -DarchetypeVersion=23-SNAPSHOT

Note: The profile "adobe-public" must be activated when using profiles like "autoInstallPackage" mentioned above.
