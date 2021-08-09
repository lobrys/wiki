We welcome everyone that wants to contribute to Spring Security in some way, either submitting a Pull Request, creating an issue ticket, asking questions, and even reviewing other's Pull Requests. But, to be able to maintain the code standard that Spring Security has, we created this guideline to help you to be aware of what to expect from and how to do a code review.
  
_This document brings recommendations to help us performing code reviews, it's not supposed to be interpreted as rules set in stone._  
  
# Code of Conduct  
  
Please see our [code of conduct](https://github.com/spring-projects/.github/blob/main/CODE_OF_CONDUCT.md).


# Contribution Guidelines

We have a [CONTRIBUTING](https://github.com/spring-projects/spring-security/blob/main/CONTRIBUTING.adoc) document that helps you to get started with the Spring Security project. It is important that you are familiar with it as it includes common stuff to pay attention when doing a code review.

# Review locally

While it is totally possible to review a PR using only the GitHub's UI, sometimes we can only have a more deep insight of the code when experimenting with it locally. Running the tests, simulating the behaviour by debugging the code are some ideas to do.

### Checking out the PR locally using Git

Checkout the PR locally:

`$ git fetch https://github.com/spring-projects/spring-security pull/xxxx/head:pull/xxxx`

`$ git checkout pull/xxxx`

Update a local copy of the PR:

`$ git checkout pull/xxxx`

`$ git pull https://github.com/spring-projects/spring-security pull/xxxx/head`

Where `xxxx` is the number of the PR.

# Dedicate your time

When performing a code review, try to dedicate the corresponding time to the PR's size. For example, if a PR is proposing a new API with thousands new lines, we should be aware that this review is going to take a while and we have to prepare ourselfs to try to review it in its entirety.
If you have to stop the review and come back after a while, almost always we can not remember where we were and we have to start over again.

Performing a full code review also helps the submitters by having less rounds of working on the feedbacks.