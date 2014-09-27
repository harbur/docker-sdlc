<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [Introduction](#introduction)
- [Code Hosting](#code-hosting)
  - [GitLab](#gitlab)
    - [QuickStart](#quickstart)
  - [GitBucket](#gitbucket)
    - [QuickStart](#quickstart-1)
- [Continuous Integration](#continuous-integration)
  - [Jenkins](#jenkins)
    - [QuickStart Latest](#quickstart-latest)
    - [QuickStart LTS](#quickstart-lts)
    - [QuickStart Harbur](#quickstart-harbur)
- [Project Management](#project-management)
  - [Redmine](#redmine)
    - [QuickStart](#quickstart-2)
    - [QuickStart Harbur](#quickstart-harbur-1)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Introduction

Docker-based multi-container Software Development Life Cycle environment.

It contains solutions of the following sections:

* Code Hosting
* Project Management
* Continuous Integration
* Continuous Inspection
* Repository Management

# Code Hosting

## GitLab

> [GitLab](https://about.gitlab.com/) offers git repository management, code reviews, issue tracking, activity feeds, wikis.

Usable Containers

|ID        |Container                                                                                                |App Version    |Size   |
|----------|---------------------------------------------------------------------------------------------------------|:-------------:|------:|
|gitlab    |[![Badge](http://dockeri.co/image/sameersbn/gitlab)](https://github.com/sameersbn/docker-gitlab)         |`v7.3.1-3`     |729.5MB|
|postgresql|[![Badge](http://dockeri.co/image/orchardup/postgresql)](https://github.com/orchardup/docker-postgresql) |latest         |488.6MB|
|redis     |[![Badge](http://dockeri.co/image/_/redis)](https://registry.hub.docker.com/_/redis/)                    |`v2.8.9`       | 98.7MB|

Topology

|Service             |Database  |Redis|
|--------------------|----------|-----|
|gitlab              |postgresql|redis|
| &#x2937; postgresql|          |     |
| &#x2937; redis     |          |     |

### QuickStart


To launch GitLab

<pre>
cd gitlab
fig up -d
echo "GitLab can be accessed at: $(docker port gitlab_gitlab_1 80)"
fig logs
</pre>

Login using the default username and password:

* username: **root**
* password: **5iveL!fe**

![GitLab](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/GitLab.png "GitLab")

To stop GitLab

<pre>
fig stop
</pre>

To remove GitLab

**WARNING**: You'll loose your data after this command

<pre>
fig kill
fig rm
</pre>

To launch more than one GitLab instances on the same host

<pre>
fig -p gitlab1 up -d
fig -p gitlab2 up -d
echo "GitLab 1 can be accessed at: $(docker port gitlab1_gitlab_1 80)"
echo "GitLab 2 can be accessed at: $(docker port gitlab2_gitlab_1 80)"
</pre>

**NOTE**: These instances do not share anything, new redis & postgresql instances are launched for each one separately.

## GitBucket

> [GitBucket](https://github.com/takezoe/gitbucket) The easily installable Github clone powered by Scala

Usable Containers

|ID        |Container                                                                                             |App Version    |Size   |
|----------|------------------------------------------------------------------------------------------------------|:-------------:|------:|
|gitbucket |[![Badge](http://dockeri.co/image/f99aq8ove/gitbucket)](https://github.com/f99aq8ove/docker-gitbucket)|`v2.2.1`       |376.2MB|

### QuickStart

To launch GitBucket

<pre>
cd gitbucket
fig up -d
echo "GitBucket can be accessed at: $(docker port gitbucket_gitbucket_1 8080)"
fig logs
</pre>

Login using the default username and password:

* username: **root**
* password: **root**

![GitBucket](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/GitBucket.png "GitBucket")

# Project Management

## Redmine

> [Redmine](http://www.redmine.org/) is a flexible project management web application

Usable Containers

|ID           |Container                                                                                               |App Version|Size   |
|-------------|--------------------------------------------------------------------------------------------------------|:---------:|------:|
|redmine      |[![Badge](http://dockeri.co/image/sameersbn/redmine)](https://github.com/sameersbn/docker-redmine)      |`v2.5.2-2` |997.9MB|
|postgresql   |[![Badge](http://dockeri.co/image/orchardup/postgresql)](https://github.com/orchardup/docker-postgresql)|latest     |488.6MB|
|redmineHarbur|[![Docker Repository on Quay.io](http://img.shields.io/badge/container-quay.io%2Fharbur%2Fredmine-blue.svg)](http://docs.harbur.io/en/latest/applications/redmine/index.html)|`v2.5.2-2` |998.1MB|


Topology

|Service             |Database  |
|--------------------|----------|
|redmine             |postgresql|
| &#x2937; postgresql|          |
|redmineHarbur       |          |
| &#x2937; postgresql|          |

### QuickStart

To launch Redmine

<pre>
cd redmine
fig up -d redmine
echo "Redmine can be accessed at: $(docker port redmine_redmine_1 80)"
fig logs
</pre>

Login using the default username and password:

* username: **admin**
* password: **admin**

![Redmine](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/Redmine.png "Redmine")

### QuickStart Harbur

Extra Features

* Preconfigured Gitmike Theme
* Preconfigured SMTP
* Dynamically configured FQDN (Injected with FQDN variable)

To launch the Harbur Redmine version run:

<pre>
cd redmine
docker login quay.io               # You need a Harbur TOKEN to access the containers
FQDN=redmine.mydomain.com fig up -d redmineHarbur
echo "Redmine can be accessed at: $(docker port redmine_redmineHarbur_1 80)"
fig logs
</pre>

Login using the default username and password:

* username: **admin**
* password: **admin**

![RedmineHarbur](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/RedmineHarbur.png "RedmineHarbur")

# Continuous Integration

## Jenkins

> [Jenkins](http://jenkins-ci.org/) An extendable open source continuous integration server

Usable Containers

|ID           |Container                                                                                                  |App Version    |Size   |
|-------------|-----------------------------------------------------------------------------------------------------------|:-------------:|------:|
|jenkinsLatest|[![Badge](http://dockeri.co/image/aespinosa/jenkins)](https://github.com/aespinosa/docker-jenkins)         |latest `v1.581`|471.3MB|
|jenkinsLTS   |[jenkins](https://registry.hub.docker.com/_/jenkins/)                                                      |LTS `v1.565.2` |  699MB|
|jenkinsHarbur|[![Docker Repository on Quay.io](http://img.shields.io/badge/container-quay.io%2Fharbur%2Fjenkins-blue.svg)](http://docs.harbur.io/en/latest/applications/jenkins/index.html)[]()|latest `v1.581`|  548MB|
|jenkinsSlave |[![Badge](http://dockeri.co/image/spiddy/dind-jenkins-slave)](https://github.com/spiddy/dind-jenkins-slave)|-              |891.5MB|

|Service               |Workers     |
|--------------------  |------------|
|jenkinsLatest         |jenkinsSlave|
|jenkinsLTS            |            |
|jenkinsHarbur         |            |
| &#x2937; jenkinsSlave|            |

### QuickStart Latest

To launch the *latest* Jenkins version run:

<pre>
cd jenkins
fig up -d jenkinsLatest
echo "Jenkins can be accessed at: $(docker port jenkins_jenkinsLatest_1 8080)"
</pre>

Jenkins is by default unsecured. Make sure to go to `Manage Jenkins - Setup Security` to configure your security.

![Jenkins Latest](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/JenkinsLatest.png "Jenkins Latest")

### QuickStart LTS

To launch the *LTS* Jenkins version run:

<pre>
cd jenkins
fig up -d jenkinsLTS
echo "Jenkins can be accessed at: $(docker port jenkins_jenkinsLTS_1 8080)"
</pre>

Jenkins is by default unsecured. Make sure to go to `Manage Jenkins - Setup Security` to configure your security.

![Jenkins LTS](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/JenkinsLTS.png "Jenkins LTS")

Current LTS Issues:

* [Failed to listen to incoming slave connection](https://github.com/cloudbees/jenkins-ci.org-docker/issues/6)

### QuickStart Harbur

Extra Features

* Pre-installed well-known plugins
* Pre-installed theme `jenkins-attlassian-theme`
* Multi-container setup with docker-aware build workers capable to auto-register themselves

To launch the Harbur Jenkins version run

<pre>
cd jenkins
docker login quay.io               # You need a Harbur TOKEN to access the containers
fig -d jenkinsHarbur jenkinsSlave
echo "Jenkins can be accessed at: $(docker port jenkins_jenkinsHarbur_1 8080)"
</pre>

Jenkins is by default unsecured. Make sure to go to `Manage Jenkins - Setup Security` to configure your security.

![Jenkins Harbur](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/JenkinsHarbur.png "Jenkins Harbur")

This is a multi-container setup with one Jenkins docker-aware slave connected dynamically to Jenkins master.
The Jenkins slave is running in privileged mode and can run docker commands attached to the host's docker remote API.

In case more slave instances are needed you can scale dynamically with the following command:

<pre>
fig -f jenkins.yml scale jenkinsSlave=2
</pre>

# Continuous Inspection

## SonarQube

> [SonarQube](http://www.sonarqube.org/) is a flexible project management web application

Usable Containers

|ID             |Container                                                                                               |App Version|Size   |
|---------------|--------------------------------------------------------------------------------------------------------|:---------:|------:|
|sonarqube      |[![Badge](http://dockeri.co/image/harbur/docker-sonarqube)](https://github.com/harbur/docker-sonarqube) |`v4.4`     |841.6MB|
|postgresql     |[![Badge](http://dockeri.co/image/orchardup/postgresql)](https://github.com/orchardup/docker-postgresql)|latest     |488.6MB|

Topology

|Service             |Database  |
|--------------------|----------|
|sonarqube           |postgresql|
| &#x2937; postgresql|          |

### QuickStart

To launch SonarQube run

<pre>
cd sonarqube
fig up
echo "SonarQube can be accessed at: $(docker port sonarqube_sonarqube_1 9000)"
fig logs
</pre>

Login using the default username and password:

* username: **admin**
* password: **admin**

![SonarQube](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/SonarQube.png "SonarQube")