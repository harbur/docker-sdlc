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

|ID        |Container                                                                                                |App Version    |Size    |
|----------|---------------------------------------------------------------------------------------------------------|:-------------:|-------:|
|gitlab    |[![Badge](http://dockeri.co/image/sameersbn/gitlab)](https://github.com/sameersbn/docker-gitlab)         |`v7.3.1-3`     |729.5 MB|
|postgresql|[![Badge](http://dockeri.co/image/orchardup/postgresql)](https://github.com/orchardup/docker-postgresql) |latest         |488.6 MB|
|redis     |[redis](https://registry.hub.docker.com/_/redis/)                                                        |`v2.8.9`       | 98.7 MB|

Topology

|Service             |Database  |Redis|
|--------------------|----------|-----|
|gitlab              |postgresql|redis|
| &#x2937; postgresql|          |     |
| &#x2937; redis     |          |     |

### QuickStart

![GitLab](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/GitLab.png "GitLab")

To launch GitLab

<pre>
fig -f gitlab.yml up -d
echo "GitLab can be accessed at: $(docker port dockersdlc_gitlab_1 80)"
fig -f gitlab.yml logs
</pre>

To stop GitLab

<pre>
fig -f gitlab.yml stop
</pre>

To remove GitLab

*WARNING*: You'll loose your data after this command

<pre>
fig -f gitlab.yml kill
fig -f gitlab.yml rm
</pre>

To launch more than one GitLab instance on same host

<pre>
fig -f gitlab.yml -p gitlab1 up -d
fig -f gitlab.yml -p gitlab2 up -d
echo "GitLab 1 can be accessed at: $(docker port gitlab1_gitlab_1 80)"
echo "GitLab 2 can be accessed at: $(docker port gitlab2_gitlab_1 80)"
</pre>

*NOTE*: These instances do not share anything, new redis & postgresql instances are launched for each one separately.

## GitBucket

> [GitBucket](https://github.com/takezoe/gitbucket) The easily installable Github clone powered by Scala

Usable Containers

|ID        |Container                                                                                             |App Version    |Size    |
|----------|------------------------------------------------------------------------------------------------------|:-------------:|-------:|
|gitbucket |[![Badge](http://dockeri.co/image/f99aq8ove/gitbucket)](https://github.com/f99aq8ove/docker-gitbucket)|`v2.2.1`       |376.2 MB|

### QuickStart

![GitBucket](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/GitBucket.png "GitBucket")

To launch GitBucket

<pre>
fig -f gitbucket.yml up -d
echo "GitBucket can be accessed at: $(docker port dockersdlc_gitbucket_1 8080)"
fig -f gitbucket.yml logs
</pre>

# Project Management

## Redmine

> [Redmine](http://www.redmine.org/) is a flexible project management web application

Usable Containers

|ID           |Container                                                                                               |App Version|Size    |
|-------------|--------------------------------------------------------------------------------------------------------|:---------:|-------:|
|redmine      |[![Badge](http://dockeri.co/image/sameersbn/redmine)](https://github.com/sameersbn/docker-redmine)      |`v2.5.2-2` |997.9 MB|
|postgresql   |[![Badge](http://dockeri.co/image/orchardup/postgresql)](https://github.com/orchardup/docker-postgresql)|latest     |488.6 MB|
|redmineHarbur|[quay.io/harbur/redmine](http://docs.harbur.io/en/latest/applications/redmine/index.html)               |`v2.5.2-2` |998.1 MB|

Topology

|Service             |Database  |
|--------------------|----------|
|redmine             |postgresql|
| &#x2937; postgresql|          |
|redmineHarbur       |          |
| &#x2937; postgresql|          |

### QuickStart

![Redmine](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/Redmine.png "Redmine")

To launch Redmine

<pre>
fig -f redmine.yml up -d redmine
echo "Redmine can be accessed at: $(docker port dockersdlc_redmine_1 80)"
fig -f redmine.yml logs
</pre>

### QuickStart Harbur

![RedmineHarbur](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/RedmineHarbur.png "RedmineHarbur")

To launch the Harbur Redmine version run:

<pre>
docker login quay.io               # You need a Harbur TOKEN to access the containers
FQDN=redmine.mydomain.com fig -f redmine.yml up -d redmineHarbur
echo "Redmine can be accessed at: $(docker port dockersdlc_redmineHarbur_1 80)"
fig -f redmine.yml logs
</pre>

Extra Features

* Preconfigured Gitmike Theme
* Preconfigured SMTP
* Dynamically configured FQDN (Injected with FQDN variable)

# Continuous Integration

## Jenkins

> [Jenkins](http://jenkins-ci.org/) An extendable open source continuous integration server

Usable Containers

|ID           |Container                                                                                                  |App Version    |Size    |
|-------------|-----------------------------------------------------------------------------------------------------------|:-------------:|-------:|
|jenkinsLatest|[![Badge](http://dockeri.co/image/aespinosa/jenkins)](https://github.com/aespinosa/docker-jenkins)         |latest `v1.581`|471.3 MB|
|jenkinsLTS   |[jenkins](https://registry.hub.docker.com/_/jenkins/)                                                      |LTS `v1.565.1` |670.8 MB|
|jenkinsHarbur|[quay.io/harbur/jenkins](http://docs.harbur.io/en/latest/applications/jenkins/index.html)                  |LTS `v1.565.1` |715.4 MB|
|jenkinsSlave |[![Badge](http://dockeri.co/image/spiddy/dind-jenkins-slave)](https://github.com/spiddy/dind-jenkins-slave)|-              |891.5 MB|

Topology

|Service               |Workers     |
|--------------------  |------------|
|jenkinsLatest         |jenkinsSlave|
|jenkinsLTS            |            |
|jenkinsHarbur         |            |
| &#x2937; jenkinsSlave|            |

### QuickStart Latest

![Jenkins Latest](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/JenkinsLatest.png "Jenkins Latest")

To launch the latest Jenkins version run:

<pre>
fig -f jenkins.yml up -d jenkinsLatest
</pre>

To identify the assigned port run:

<pre>
fig -f jenkins.yml ps
</pre>

The assigned port for 8080 is the web interface. Open it on the web browser to connect to Jenkins. To find the port programmatically run:

<pre>
docker port dockersdlc_jenkinsLatest_1 8080
</pre>

### QuickStart LTS

![Jenkins LTS](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/JenkinsLTS.png "Jenkins LTS")

To launch the LTS Jenkins version run:

<pre>
fig -f jenkins.yml up -d jenkinsLTS
docker port dockersdlc_jenkinsLTS_1 8080
</pre>


Current LTS Issues:

* [Failed to listen to incoming slave connection](https://github.com/cloudbees/jenkins-ci.org-docker/issues/6)

### QuickStart Harbur

![Jenkins Harbur](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/JenkinsHarbur.png "Jenkins Harbur")

To launch the Harbur Jenkins version run:

<pre>
docker login quay.io               # You need a Harbur TOKEN to access the containers
fig -f jenkins.yml -d jenkinsHarbur jenkinsSlave
docker port dockersdlc_jenkinsHarbur_1 8080
</pre>

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

|ID             |Container                                                                                               |App Version|Size    |
|---------------|--------------------------------------------------------------------------------------------------------|:---------:|-------:|
|sonarqube      |[harbur/sonarqube](harbur/sonarqube:latest)                                                             |`v4.4`     |  871 MB|
|postgresql     |[![Badge](http://dockeri.co/image/orchardup/postgresql)](https://github.com/orchardup/docker-postgresql)|latest     |488.6 MB|

Topology

|Service             |Database  |
|--------------------|----------|
|sonarqube           |postgresql|
| &#x2937; postgresql|          |

### QuickStart

![SonarQube](https://raw.githubusercontent.com/harbur/docker-sdlc/master/images/SonarQube.png "SonarQube")

To launch SonarQube

<pre>
fig -f sonarqube.yml up
echo "SonarQube can be accessed at: $(docker port dockersdlc_sonarqube_1 9000)"
fig -f sonarqube.yml logs
</pre>
