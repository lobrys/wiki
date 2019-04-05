## Perform a Milestone, RC or GA Release

**NOTE:** This release process uses the [spring-build-conventions](https://github.com/spring-gradle-plugins/spring-build-conventions) gradle plug-in. 

### Process Overview

1. Update dependencies
2. Update release version
3. Push the release commit
4. Announce the release on Slack
5. Tag the release
6. Update to next development version
7. Update version on project page
8. Close / Create Milestone
9. Announce the release on other channels

### Detailed Steps

#### 1. Update dependencies

- Dependencies are declared in `gradle/dependency-management.gradle`
- Update Spring Framework and Spring Data at a minimum
- Then find dependencies that need updating by running the following commands:
    - `./gradlew dependencyUpdates -Drevision=release`
    - `find . -name report.txt | xargs cat > dep-updates.txt`
    - `cat dep-updates.txt | fgrep ' ->' | sort | uniq`

#### 2. Update release version
 
- Update the version number in `gradle.properties` for the release, for example, `5.1.0.M1`, `5.1.0.RC1`, `5.1.0.RELEASE` 

#### 3. Push the release commit
 
- Push the release commit and [Jenkins](https://jenkins.spring.io/job/spring-security/) will build and deploy the artifacts
- If you would like to be notified when the artifacts are deployed to Maven Central, modify the version in the following script and run it:
    - `until http -h --check-status http://repo1.maven.org/maven2/org/springframework/security/spring-security-core/5.1.5.RELEASE/; do sleep 10; done; say "It is now uploaded";`

#### 4. Announce the release on Slack

- Announce via Slack on [#spring-security](https://pivotal.slack.com/messages/spring-security) and cc Andy Wilkinson, Gary Russell and Artem Bilan

#### 5. Tag the release

- Tag the release and then push the tag

#### 6. Update to next development version
 
- Update release version to next `BUILD-SNAPSHOT` version and then push

#### 7. Update version on project page

- Update release version on [projects.spring.io](https://spring.io/admin/projects/spring-security)

#### 8. Close / Create Milestone

- In [GitHub Milestones](https://github.com/spring-projects/spring-security/milestones), 
create a new milestone for the next release version and move any open issues 
from the existing milestone you just released to the new milestone and then close the milestone for the release.

#### 9. Announce the release on other channels

- Create a [Blog](https://spring.io/admin/blog)
- Tweet from [@SpringSecurity](https://twitter.com/springsecurity)
- Send email to spring-developer@pivotal.io
