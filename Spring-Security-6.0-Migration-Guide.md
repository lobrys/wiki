This document is meant to help you migrate your application to Spring Security 6.0.

# Before You Start

If you are using Spring Boot, consider reading the [Spring Boot 3.0 Migration Guide](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide).

## Upgrade to the Latest `5.8.x` Version

Before you start the upgrade, make sure to upgrade to the latest available `5.8.x` version. This will make sure that you are building against the most recent dependencies of that line.

The `5.8.x` is a special release that was designed to help you to migrate to Spring Security 6.0. Spring Boot `2.7.x`, the latest release in the `2.x` line, does not use Spring Security `5.8.x`, because of that, you have to [override the dependency versions manually](https://docs.spring.io/spring-security/reference/5.8/getting-spring-security.html).

## Review Deprecations

There are several deprecations that were removed in 6.0 that should be replaced in `5.8.x`. To help with that, you can read the [Prepare for 6.0](https://docs.spring.io/spring-security/reference/5.8.2/migration/index.html) section of the documentation and apply the suggested changes.

# Upgrade to Spring Security 6.0

After you upgraded to `5.8.x` and all the necessary changes were applied to your application by following the [Prepare for 6.0](https://docs.spring.io/spring-security/reference/5.8.2/migration/index.html) documentation, you are now ready to upgrade to 6.0.

If you are using Spring Boot, you should [upgrade it to 3.0](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-3.0-Migration-Guide#upgrade-to-spring-boot-3). Otherwise, you can follow the instructions [here](https://docs.spring.io/spring-security/reference/getting-spring-security.html).

After upgrading the dependency versions, please refer to [Migrating to 6.0](https://docs.spring.io/spring-security/reference/migration/index.html) to perform any remaining migration or cleanup steps.

