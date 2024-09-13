### Pipeline Configuration for Bitbucket

This repository contains two Bitbucket pipelines that automate the deployment process for Mule applications. The pipelines are designed for two different environments: **CloudHub** and **On-Premises Servers**. Below are the details of each pipeline:

---

#### 1. `bitbucket-pipelines.yml` - Deploy to CloudHub

This pipeline handles the deployment of Mule applications to **CloudHub**. It consists of three main steps:

- **Create and Execute the Script to Update the POM**: This step configures and updates the `pom.xml` file with the necessary CloudHub deployment configuration.
  
- **Build**: The application is built using Maven.

- **Deploy to CloudHub**: The final step deploys the application to the CloudHub environment.

The process also covers:
- The creation of a Bitbucket repository with three branches (`develop`, `staging`, `product`).
- Configuration of environment variables.
- Integration of the required configuration file (`bitbucket-pipelines.yml`) into each branch to automate the update, build, and deployment processes for CloudHub environments.

---

#### 2. `bitbucket-pipelines_on_premises.yml` - Deploy to On-Premises Servers

This pipeline is designed for the deployment of Mule applications to **On-Premises Servers**. It also consists of three main steps:

- **Create and Execute the Script to Update the POM**: This step configures the `pom.xml` file with the necessary settings for deployment on on-premises servers.

- **Build**: The application is built using Maven.

- **Deploy to On-Premises Server**: The final step deploys the application to the configured on-premises environment.

The process includes:
- Server configuration in the Runtime Manager.
- Addition of necessary environment variables.
- Implementation of a generic Bitbucket pipeline that automates the update of the `pom.xml`, builds the application, and deploys it to the on-premises servers. Special attention is given to secure management of configurations through a separate `config.env` file.

---

Both pipelines ensure seamless deployment across different environments, allowing for flexibility in application management and deployment.
