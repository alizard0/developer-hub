# Developer Hub Guide

The internal developer platform (IdP) aims to reduce the cognitive load from the developers, making their work easier by abstracting away infrastructure, deployment, tooling and pipelines. 

Recently, many companies created platform teams which are responsible to abstract the infrastructure and operations from the development teams. This teams make sure that the platform (kubernetes, cloud services or virtual machines) are up and ready to be used in development, testing and production. They are not responsible for the code quality but they are responsible for the platform reliability and availability. These teams usually communicate with the development teams through Service Now tickets or Confluence pages which are the available tools within the companies, unfortunately these tools were not built to meet the Platform Engineering needs.

### How can you measure the impact of having an Internal Developer Platform in your company? 

The best way metrics to answer this question are Mean Time To Recovery (MTTR) and Change Failure Rate (CFR). 

1. MTTR measures the average time that takes to restore a failed system. It relies on another set of metrics like reliability and maintainability!

2. Change Failure Rate (CFR) measures the number of code changes that result in a failure (during deployment or at runtime) or a loss of service in production.

### How can you get better metrics out of the IdP?

IdP promotes ownership across the development eam by allowing developers to create, develop, deploy, maintain and debug projects without opening JIRA or SNOW tickets, or starting huge email threads that might take weeks to close.

### What is the difference between a Developer/Service Portal and an IdP?

Developer/Service Portals provide only a subset of the IdP features. Such portals allow developers to subscribe APIs, to renew authentication tokens, to promote APIs through different environments up to production, to set consumption rates, to disable/enable features or even to administrate a set of web APIs. As describe above, in the Architecture section, an IdP covers much more areas, it did not only focus on the management or maintainability of the application, it goes down on the stack, allowing the developer to create, develop, test, deploy and maintain their application by setting their infrastructure as a code, creating application configuration and secrets, pushing the code through the pipeline and collaborate all the time with the platform team.

## Architecture

![](https://redhatquickcourses.github.io/devhub-intro/nolinks/devhub-intro/1/introduction/_images/rhdh-architecture.png)

An IdP should cover five areas that affect the entire software lifecycle: Application Configuration Management, Infrastructure Orchestration, Environment Management, Deployment Management and Role-Based Access Control.

1. Application Configuration Management is the component that allows the developer to manage their application configuration as a code which includes: secrets, versioning and environment settings.

2. Infrastructure Orchestration integrates the Continuous Integration pipelines, Clusters (Kubernetes or Virtual Machines), Domain Name Servers and be able to manage all infrastructure needed through Infrastructure as a Code.

3. Enviroment Management allows the development team to fully provision environments on demand without requesting it to the platform, operations or infrastructure team.

4. Deployment Management enables the development team to a Continuous Deployment mindset and keeps record of every deployment made.

5. Role-Based Access Control is an important feature not for the development team but for the Platform/Operations team which will be able to limit access (viewer/editor/owner) by environment, resource or application to any group/users.

### Software Components

1. The core (node.js runtime) consists of basic functionality like configuration, logging, plugin lifecycle control, scheduled jobs and more.

2. The web-ui is a react application written in TypeScript that integrates with the backend api. The user interface uses Material UI and can be customized using html, css and typescript.

3. The backend is a node.js application written in typescript and express.js framework. It exposes the features of the IDP as a REST API that can be consumed by the front-end. 

4. The application data is stored in a PostgreSQL running on Openshift.

5. The plugins can be purely front-end based which can integrate with third party APIs. They can also combine front and back end.

6. The application is depoyed on Openshift and ties together core functionality provided by the platform with additional plugins. The application is built and maintained by the platform engineering teams to serve their customers. The application is configured using YAML files.

![](https://backstage.io/assets/images/backstage-typical-architecture-c38b04130f70f294725a9f646df94d3a.png)

### Package Architecture

Backstage relies heavily on NPM packages, both for distribution of libraries and structuring of code within projects.

![](https://backstage.io/assets/images/package-architecture.drawio-15aac8979d89a6c2f7eb24f04d8d3b32.svg)

- The arrows indicate a runtime dependency on the code of the target package.
- The app and backend packages are the entry points of a Backstage project. The app package is the front end application that brings together a collection of frontend plugins. The backend pacakge is the backend service that powers the application.

#### Plugin Package

1. A typical plugin consists in five packages> two backend, two frontend and one isomorphic package. All packages within the plugin must share a common prefix - `@<scope>/plugin-<plugin-id>`

1. Along with this prefix, each package have their own unique suffix that denotes their role. 

1. The `-react`, `-common` and `-node` make the external library of a plugin. The plugin library enables other plugins to build on top of and extend aplugin.

#### Frontend Package

The frontend package are grouped in `frontend app core` which is a set of packages that are only used by the app package itselft to build up the core structure. And by the rest of the shared packages called `frontend plugin core` and `frontend libraries`.

#### Backend Packages

The backend library packages do not currently share a similar plugin architecture as the frontend packages. Tehy are instead simply a collection of building blocks and patterns that help you build backend services.

#### Common Packages

The common packages are the packages that depended on by  all other pages.



### Backstage, Project Janus and Red Hat Developer Hub

![](https://redhatquickcourses.github.io/devhub-intro/nolinks/devhub-intro/1/introduction/_images/backstage-janus-rhdh-flow.png)

1. [Backstage](https://backstage.io/) provides the core features for building developer portals, and supports plugins for extend its capabilities (platform, runtime and external APIs). Usually, Platform Teams start with Backstage and customize it using their own developed plugins.

2. [Project Janus](https://janus-idp.io/blog) is a community to share Backstage plugins that can be installed on Openshift and that are mainly targeted to be used with Red Hat products.

3. [Red Hat Developer Hub](https://docs.redhat.com/en/documentation/red_hat_developer_hub/1.6) is an enterprise developer portal for deploying on Openshift, for building, integrating and testing container images, for integrating GitOps, Tekton Pipelines, Registry and Authentication.

![](https://redhatquickcourses.github.io/devhub-intro/nolinks/devhub-intro/1/introduction/_images/rhdh-big-picture.png)

#### Red Hat Developer Hub

![](https://redhatquickcourses.github.io/devhub-intro/nolinks/devhub-intro/1/features/_images/rhdh-core-features.png)

1. Enables collaboration across development, platform and operation teams.

2. Unified dashboard for Git, CI/CD, Secure Software Supply Chain, Openshift Clusters, JIRA, Git Issues, Monitoring, API, Documentation and so on.

3. Apply organization architectural practices for creating, testing and deploying applications.

4. Sharable, maintanable and accessible technical documentation across development, platform and operations teams.

5. Smooth onboarding experiences for new developers.

6. Robust RBAC.

