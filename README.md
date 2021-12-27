# Pokedox

This is a simple pokemon finding application designed in compose and implemented cache funtionality.

## What's Included in the applications

A number of third party dependencies are included in this template. They are also documented inside the [documentation folder](/documentation). The files inside this documentation folder are written in such a way that you can keep them in your real project, to let team members read up on why dependencies are included and how they work.

The dependencies in the template include:

* [Ktlint](/documentation/StaticAnalysis.md) for formatting.
* [Detekt](/documentation/StaticAnalysis.md) for code smells.
* [Git Hooks](/documentation/GitHooks.md) for automatically perform static analysis checks. 
* [Gradle Versions Plugin](/documentation/VersionsPlugin.md) for checking all dependencies for new versions.
* [GitHub Actions](/documentation/GitHubActions.md) for running continuous integration and ensuring code quality with every PR.

### Danger

This template uses [Danger](https://danger.systems) which will perform some checks against our 
pull requests. You can find the list of checks in the [Dangerfile](Dangerfile). In addition, we 
have a GitHub Actions workflow for Danger checks. In order for that to work, you'll need a 
Danger API key setup in your GitHub secrets. Info on this can be found [here](https://www.jessesquires.com/blog/2020/04/10/running-danger-on-github-actions/). 

## Dependency Setup

You may notice that dependencies are set up in a very specific way. Each of the tools has its own Gradle file in the [buildscripts folder](/buildscripts). This is by design so that if you chose to have a multi module project, these dependencies can easily be shared between them. This is already configured inside our root `build.gradle` file, by applying to each sub project:

```groovy
subprojects {
    apply from: "../buildscripts/ktlint.gradle"
    apply from: "../buildscripts/detekt.gradle"
    apply from: "../buildscripts/versionsplugin.gradle"
}
```

In addition, there is a [versions.gradle](/buildscripts/versions.gradle) file which includes the version numbers of all dependencies used inside the app module. The benefit of moving them here, is that if any dependencies are shared between two modules, we only have to update the version number in one spot. As an added bonus, each dependency version also has a comment linking to the release page, so you can quickly reference to see what's changed. 

