# Perform a Milestone, RC or GA Release

**NOTE:** This release process uses the [spring-build-conventions](https://github.com/spring-gradle-plugins/spring-build-conventions) gradle plug-in. 

## Process Overview

1. [Update dependencies](#1-update-dependencies)
2. [Update release version](#2-update-release-version)
3. [Build Locally](#3-build-locally)
4. [Push the release commit](#4-push-the-release-commit)
5. [Announce the release on Slack](#5-announce-the-release-on-slack)
6. [Tag the release](#6-tag-the-release)
7. [Update to next development version](#7-update-to-next-development-version)
8. [Update version on project page](#8-update-version-on-project-page)
9. [Update Release Notes on GitHub](#9-update-release-notes-on-github)
10. [Close / Create Milestone](#10-close--create-milestone)
11. [Announce the release on other channels](#11-announce-the-release-on-other-channels)


## Detailed Steps

### 1. Update dependencies

If you are on master use 1.b, otherwise use 1.a

### 1.a Updating Manually

- Dependencies are declared in `gradle/dependency-management.gradle`
- Update Spring Framework and Spring Data at a minimum
- Then find dependencies that need updating by running the `update-dependencies.sh` script:
```bash
./scripts/update-dependencies.sh
```
_Prerequisites: The `build` directory has to exist to store the file `build/updates.txt`. This directory gets created when a new build is run, but is not present on a fresh git clone._

### 1.b Lock Dependencies

Master is setup to use Gradle [dependency locking](https://docs.gradle.org/current/userguide/dependency_locking.html) and version ranges so builds automatically take advantage of the latest dependencies. In order to ensure releases are reproducible, we must lock the dependencies before a release.

To lock the dependencies execute:

```
./gradlew writeLocks --write-locks
```

This writes out all the resolved versions. Run the build. If it passes, commit the changes.

### 2. Update release version
 
- Update the version number in `gradle.properties` for the release, for example, `5.1.0.M1`, `5.1.0.RC1`, `5.1.0.RELEASE` 

### 3. Build Locally

- Run the build locally with:
```bash
./gradlew check
```

### 4. Push the release commit
 
- Push the release commit and [Jenkins](https://jenkins.spring.io/job/spring-security/) will build and deploy the artifacts
- If you are pushing to Maven Central, then you can get notified when it's uploaded by running the following:
```bash
./scripts/release/wait-for-done.sh 5.2.0.RELEASE
```

### 5. Announce the release on Slack

- Announce via Slack on [#spring-security](https://pivotal.slack.com/messages/spring-security), including the keyword `spring-security-release` in the message. Something like:
```
spring-security-release 5.2.0.RC1 is out!
```

### 6. Tag the release

- Tag the release and then push the tag
```
git tag 5.2.0.RC1
git push origin 5.2.0.RC1
```

### 7. Update to next development version
 
- Update release version to next `BUILD-SNAPSHOT` version and then push
- If dependency locks (1.b) were used, revert the commit that included the lock files so that the build uses the latest versions again.

### 8. Update version on project page

- Update release version on [projects.spring.io](https://spring.io/admin/projects/spring-security)

### 9. Update Release Notes on GitHub

- Download [the GitHub release notes generator](https://github.com/spring-io/github-release-notes-generator/releases/latest)
```
wget https://github.com/spring-io/github-release-notes-generator/releases/download/v0.0.2/github-release-notes-generator.jar
```

- Generate the release notes
```
java -jar github-release-notes-generator.jar \
    --releasenotes.github.organization=spring-projects \
    --releasenotes.github.repository=spring-security \
    --spring.config.location=scripts/release/release-notes-sections.yml \
    $MILESTONE release-notes
```
Note 1: `$MILESTONE` is something like `5.2.1` or `5.3.0.M1`.  
Note 2: The location `scripts/release/release-notes-sections.yml` is relative to the `spring-security` repo.  
Note 3: This will create a file on your filesystem called `release-notes`.  

- Copy the release notes to your clipboard (your mileage may vary with the following command)
```
cat release-notes | xclip -selection clipboard
```

- Create the [release on GitHub](https://github.com/spring-projects/spring-security/releases), associate it with the tag, and paste the generated notes

### 10. Close / Create Milestone

- In [GitHub Milestones](https://github.com/spring-projects/spring-security/milestones), 
create a new milestone for the next release version
- Move any open issues from the existing milestone you just released to the new milestone
- Close the milestone for the release.

### 11. Announce the release on other channels

- Create a [Blog](https://spring.io/admin/blog)
- Tweet from [@SpringSecurity](https://twitter.com/springsecurity)
- Send email to spring-developer@pivotal.io
