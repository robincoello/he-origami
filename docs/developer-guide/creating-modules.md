---
layout: default
title: Creating modules
section: Developer guide
permalink: /docs/developer-guide/creating-modules/
---

# Creating new Origami modules

Begin by following the instructions for the [origami-build-tools](https://github.com/Financial-Times/origami-build-tools) (if not already installed) and the [o-component-blueprint](https://github.com/Financial-Times/o-component-blueprint) component. When complete, you will have installed the local development tools and established the project structure for the new component.

## Source control

Where possible, Origami components should be released publicly via [GitHub](https://github.com/pearson-higher-ed). When deciding whether or not to release a component publicly, you _must_ understand and follow the [open source policy](). Internal components may be released to the [HE Origami Components](https://devops-tools.pearson.com/stash/projects/ORC) project in Stash. You will need to make a request for creation of a new repository from one of the owners or project administrators of the GitHub organization or Stash project, respectively.

## Continuous Integration

Any [module](/docs/component-spec/modules/#module-components) component that is released publicly via GitHub and that implements [continuous integration](http://localhost:4000/docs/component-spec/modules/#continuous-integration) _must_ use [Travis CI](https://travis-ci.org) configured with the appropriate origami-build-tools tasks in the build script. If you created your project using the o-component-blueprint component, a default `.travis.yml` configuration file has been included for you.

<aside>
    A request to enable Travis CI for the new repository should be made to one of the GitHub organization's owners.
</aside>

## Releasing

A [module](/docs/component-spec/modules/#module-components) component release occurs when a new git tag is pushed to the remote repository. Follow the guidelines for [managing new releases](/docs/component-spec/modules/#managing-new-releases).
