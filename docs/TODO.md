# Introduction

These are some of the features I would like to include at some point; ideas that either someone else or I may think will improve the project.

#### Project Organization
* Write a style guide, disgussing and outlining project styles (example: [camelcase/caps](https://en.wikipedia.org/wiki/Camel_case#Computer_programming) vs [snakecase](https://en.wikipedia.org/wiki/Snake_case)), even though Ansible is a Python language. This is just a stylistic preference, but it should be uniform and documented.

#### Guest Enhancements
* There's really no need for the ISO to be downloaded locally (unless that is actually desired). It would be better to download straight to the `libvirtHost` in the near future, and it's easier on resources/time. / bbj - I will likely do this via a separate playbook.

#### Playbook Enhancements
* Ensure that the variable `clusterID` is recorded between playbooks, so that playbooks can be run together (example: `createAICluster` + `createAILibvirtGuestTemplates`)

#### Security Enhancements
* Consider using `ansible-vault` for pull secret