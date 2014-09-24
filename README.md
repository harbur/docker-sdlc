<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](http://doctoc.herokuapp.com/)*

- [Introduction](#introduction)
- [Continuous Integration](#continuous-integration)
  - [jenkins](#jenkins)
    - [QuickStart Latest](#quickstart-latest)
    - [QuickStart LTS](#quickstart-lts)
    - [QuickStart Harbur](#quickstart-harbur)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# Introduction

Docker-based multi-container Software Development Life Cycle environment.

It contains solutions of the following sections:

* Code Hosting
* Continuous Integration
* Project Management
* Code Analysis
* Repository Management

# Continuous Integration

## jenkins

Usable Containers

|ID           |Container                |App Version    |Size    |
|-------------|-------------------------|:-------------:|-------:|
|jenkinsLatest|aespinosa/jenkins        |latest `v1.581`|471.3 MB|
|jenkinsLTS   |jenkins                  |LTS `v1.565.1` |670.8 MB|
|jenkinsHarbur|quay.io/harbur/jenkins   |LTS `v1.565.1` |715.4 MB|
|jenkinsSlave |spiddy/dind-jenkins-slave|-              |891.5 MB|

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
