## Perform a Milestone, RC or GA Release

**NOTE:** This release process uses the [spring-build-conventions](https://github.com/spring-gradle-plugins/spring-build-conventions) gradle plug-in. 

### Process Overview

1. Update dependencies
2. Update release version
3. Push the release commit
4. Tag the release
5. Update to next development version
6. Update version on project page
7. Close / Create Milestone
8. Announce the release

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

#### 4. Tag the release

- Tag the release and then push the tag

#### 5. Update to next development version
 
- Update release version to next `BUILD-SNAPSHOT` version and then push

#### 6. Update version on project page

- Update release version on [projects.spring.io](https://spring.io/admin/projects/spring-security)

#### 7. Close / Create Milestone

- In [GitHub Milestones](https://github.com/spring-projects/spring-security/milestones), 
create a new milestone for the next release version and move any open issues 
from the existing milestone you just released to the new milestone and then close the milestone for the release.

#### 8. Announce the release

- Create a [Blog](https://spring.io/admin/blog)
- Tweet from [@SpringSecurity](https://twitter.com/springsecurity)
- Send email to spring-developer@pivotal.io
- Announce via Slack and cc Andy Wilkinson, Gary Russell and Artem Bilan
