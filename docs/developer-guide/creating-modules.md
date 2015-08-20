---
layout: default
title: Creating modules
section: Developer guide
permalink: /docs/developer-guide/creating-modules/
---

# Creating new Origami modules

Begin by following the instructions for the [origami-build-tools](https://github.com/Financial-Times/origami-build-tools) (if not already installed) and the [o-component-blueprint](https://github.com/Financial-Times/o-component-blueprint) component. When complete, you will have installed the local development tools and established the project structure for the new component.

## Using the Origami build tools

The Origami build tools provides a set of tasks for building and verifying your component and its demos. Run the tasks using the `origami-build-tools` command, or its shortened version, `obt`.

### Verifying your code

Run the `verify` and `test` tasks to validate your code. The `verify` task handles linting and code-style validation; the `test` task will run unit and other tests. Projects created using `o-component-blueprint` are configured to use the [Karma](http://karma-runner.github.io/0.13/index.html) test runner. Under normal circumstances, your component should not contain `.editorconfig` or linting settings files (`.jshintrc`, `.eslintrc`, etc). If you wish to use the standard Origami settings with editor or IDE plugins&mdash;for example, [EditorConfig](http://editorconfig.org/)&mdash;then you may link or copy the appropriate file from `origami-build-tools` into a parent directory.

### Building and running demos

During development, you will likely want to build and run the demos locally. To do so, use the `demos` task:

```
obt demo --runServer
```

This will generate the static content in the *demos/local* directory and start a server running at `localhost:8080` (or other port, if `8080` is unavailable). If you scaffolded your component using `o-component-blueprint`, then the *demos/local* directory is already included in `.gitignore`. This directory should not be committed to the repository.

Running `obt demo` will also generate HTML files in the *demos* directory. These files are used by the registry for the in-line demos and *should* be committed. Use the `--updateorigami` flag to automatically update the demo configuration in `origami.json`.

### Configuring demos

The source for all of the demos typically resides in the *demos/src* directory, including the configuration file. Refer to the [tests and demos]({{ site.baseurl }}/docs/component-spec/modules/#tests-and-demos) section of the [component specification]({{ site.baseurl }}/docs/component-spec/modules/) for additional information.

## Source control

Where possible, Origami components should be released publicly via [GitHub](https://github.com/pearson-higher-ed). When deciding whether or not to release a component publicly, you _must_ understand and follow the [open source policy]({{ site.baseurl }}/docs/developer-guide/open-source-policy/). Internal components may be released to the [HE Origami Components](https://devops-tools.pearson.com/stash/projects/ORC) project in Stash. You will need to make a request for creation of a new repository from one of the owners or project administrators of the GitHub organization or Stash project, respectively.

## Continuous Integration

Any [module]({{ site.baseurl }}/docs/component-spec/modules/#module-components) component that is released publicly via GitHub and that implements [continuous integration](http://localhost:4000/docs/component-spec/modules/#continuous-integration) _must_ use [Travis CI](https://travis-ci.org) configured with the appropriate origami-build-tools tasks in the build script. If you created your project using the o-component-blueprint component, a default `.travis.yml` configuration file has been included for you.

<aside>
    A request to enable Travis CI for the new repository should be made to one of the GitHub organization's owners.
</aside>

## Releasing

A [module]({{ site.baseurl }}/docs/component-spec/modules/#module-components) component release occurs when a new git tag is pushed to the remote repository. Follow the guidelines for [managing new releases]({{ site.baseurl }}/docs/component-spec/modules/#managing-new-releases). The registry will pick up new versions during the next automated scan.

## FAQ

- ***Should I commit `.editorconfig`, `.jshintrc`, etc. files to the repository?*** In general, no. Components *should* use the settings provided by `origami-build-tools` to ensure consistency across all modules. However, a component *may* provide overrides if absolutely necessary.
