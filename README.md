<!-- 














  ** DO NOT EDIT THIS FILE
  ** 
  ** This file was automatically generated by the `build-harness`. 
  ** 1) Make all changes to `README.yaml` 
  ** 2) Run `make init` (you only need to do this once)
  ** 3) Run`make readme` to rebuild this file. 
  **
  **















  -->


# Build Harness [![Build Status](https://travis-ci.org/sgcip/build-harness.svg?branch=master)](https://travis-ci.org/sgcip/build-harness) [![Latest Release](https://img.shields.io/github/release/sgcip/build-harness.svg)](https://github.com/sgcip/build-harness/releases/latest) [![Slack Community](https://slack.sgcip.com/badge.svg)](https://slack.sgcip.com) [![Discourse Forum](https://img.shields.io/discourse/https/ask.sgcip.com/posts.svg)](https://ask.sgcip.com/)


This `build-harness` is a collection of Makefiles to facilitate building Golang projects, Dockerfiles, Helm charts, and more.
It's designed to work with CI/CD systems such as GitHub Actions, Codefresh, Travis CI, CircleCI and Jenkins.


---

This project is part of our ["open source"](#) strategy.
[<img align="right" title="Share via Email" src="https://docs.cloudposse.com/images/ionicons/ios-email-outline-2.0.1-16x16-999999.svg"/>][share_email]
[<img align="right" title="Share on Google+" src="https://docs.cloudposse.com/images/ionicons/social-googleplus-outline-2.0.1-16x16-999999.svg" />][share_googleplus]
[<img align="right" title="Share on Facebook" src="https://docs.cloudposse.com/images/ionicons/social-facebook-outline-2.0.1-16x16-999999.svg" />][share_facebook]
[<img align="right" title="Share on Reddit" src="https://docs.cloudposse.com/images/ionicons/social-reddit-outline-2.0.1-16x16-999999.svg" />][share_reddit]
[<img align="right" title="Share on LinkedIn" src="https://docs.cloudposse.com/images/ionicons/social-linkedin-outline-2.0.1-16x16-999999.svg" />][share_linkedin]
[<img align="right" title="Share on Twitter" src="https://docs.cloudposse.com/images/ionicons/social-twitter-outline-2.0.1-16x16-999999.svg" />][share_twitter]


It's 100% Open Source and licensed under the [APACHE2](LICENSE).








## Screenshots


![demo](https://cdn.rawgit.com/cloudposse/build-harness/master/docs/demo.svg)
*Example of using the `build-harness` to build a docker image*






## Usage



At the top of your `Makefile` add, the following...

```make
-include $(shell curl -sSL -o .build-harness "https://git.io/sgcip-utils-bh"; echo .build-harness)
```

This will download a `Makefile` called `.build-harness` and include it at run-time. We recommend adding the `.build-harness` file to your `.gitignore`.

This automatically exposes many new targets that you can leverage throughout your build & CI/CD process.

Run `make help` for a list of available targets.

**NOTE:** the `/` is interchangable with the `:` in target names

## GitHub Actions

The `build-harness` is compatible with [GitHub Actions](https://github.com/features/actions).

Here's an example of running `make readme/lint` 

```
name: build-harness/readme/lint
on: [pull_request]
jobs:
  build:
    name: 'Lint README.md'
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@master
    - uses: sgcip/build-harness@master
      with:
        entrypoint: /usr/bin/make
        args: readme/lint
 ```

## Quick Start

Here's how to get started...

1. `git clone https://github.com/sgcip/build-harness.git` to pull down the repository
2. `make init` to initialize the [`build-harness`](https://github.com/sgcip/build-harness/)


## Examples

Here are some real world examples:
- [`github-authorized-keys`](https://github.com/cloudposse/github-authorized-keys/) - A Golang project that leverages `docker/%`, `go/%`, `travis/%` targets
- [`charts`](https://github.com/cloudposse/charts/) - A collection of Helm Charts that leverages `docker/%` and `helm/%` targets
- [`bastion`](https://github.com/cloudposse/bastion/) - A docker image that leverages `docker/%` and `bash/lint` targets
- [`terraform-null-label`](https://github.com/cloudposse/terraform-null-label/) - A terraform module that leverages `terraform/%` targets



## Makefile Targets
```
Available targets:

  aws/install                         Install aws cli bundle
  aws/shell                           Start a aws-vault shell with access to aws api
  bash/lint                           Lint all bash scripts
  chamber/install                     Install chamber
  chamber/shell                       Start a chamber shell with secrets exported to the environment
  codefresh/export                    DEPRECATED!!! Export codefresh additional envvars
  codefresh/notify/slack/build        Send notification from codefresh to slack using "build" template
  codefresh/notify/slack/deploy       Send notification from codefresh to slack using "deploy" template
  codefresh/notify/slack/deploy/webapp Send notification from codefresh to slack using "deploy" template with exposed endpoint
  codefresh/notify/slack/sync         Send notification from codefresh to slack using "codefresh-sync" template
  codefresh/pipeline/export           Export pipeline vars
  codefresh/sync/apply                Codefresh pipelines sync - Apply the changes
  codefresh/sync/auth/%               Authentificate on codefresh account
  codefresh/sync/deps                 Install dependencies for codefresh sync
  codefresh/sync/diff                 Codefresh pipelines sync - Show changes
  codefresh/sync/pipeline/export      Export sync pipeline vars
  codefresh/trigger/webhook           Trigger a CodeFresh WebHook
  completion/install/bash             Install completion script for bash
  compose/build                       Build local dev environment
  compose/down                        Stop local dev environment
  compose/monitor                     Show containers resource usage
  compose/monitor/follow              Monitor in time containers resource usage
  compose/purge                       Purge local dev environment
  compose/rebuild                     Rebuild custom containers for local dev environment
  compose/restart                     Restart local dev environment
  compose/top                         Show top for containers
  compose/up                          Start local dev environment (daemonized)
  docker/build                        Build docker image
  docker/clean                        Cleanup docker.                     WARNING!!! IT WILL DELETE ALL UNUSED RESOURCES
  docker/clean/containers             Cleanup docker containers.          WARNING!!! IT WILL DELETE ALL UNUSED CONTAINERS
  docker/clean/images                 Cleanup docker images.              WARNING!!! IT WILL DELETE ALL UNUSED IMAGES
  docker/clean/images/all             Cleanup docker images all.          WARNING!!! IT WILL DELETE ALL IMAGES
  docker/clean/networks               Cleanup docker networks.            WARNING!!! IT WILL DELETE ALL UNUSED NETWORKS
  docker/clean/volumes                Cleanup docker volumes.             WARNING!!! IT WILL DELETE ALL UNUSED VOLUMES
  docker/image/promote/local          Promote $SOURCE_DOCKER_REGISTRY/$IMAGE_NAME:$SOURCE_VERSION to $TARGET_DOCKER_REGISTRY/$IMAGE_NAME:$TARGET_VERSION
  docker/image/promote/remote         Pull $SOURCE_DOCKER_REGISTRY/$IMAGE_NAME:$SOURCE_VERSION and promote to $TARGET_DOCKER_REGISTRY/$IMAGE_NAME:$TARGET_VERSION
  docker/image/push                   Push $TARGET_DOCKER_REGISTRY/$IMAGE_NAME:$TARGET_VERSION
  docker/login                        Login into docker hub
  docs/copyright-add                  Add copyright headers to source code
  geodesic/deploy                     Run a Jenkins Job to Deploy $(APP) with $(CANONICAL_TAG)
  git/aliases-update                  Update git aliases
  git/export                          Export git vars
  github/download-private-release     Download release from github
  github/download-public-release      Download release from github
  github/latest-release               Fetch the latest release tag from the GitHub API
  github/push-artifacts               Push all release artifacts to GitHub (Required: `GITHUB_TOKEN`)
  gitleaks/install                    Install gitleaks
  gitleaks/scan                       Scan current repository
  git/submodules-update               Update submodules
  go/build                            Build binary
  go/build-all                        Build binary for all platforms
  go/clean                            Clean compiled binary
  go/clean-all                        Clean compiled binary and dependency
  go/deps                             Install dependencies
  go/deps-build                       Install dependencies for build
  go/deps-dev                         Install development dependencies
  go/fmt                              Format code according to Golang convention
  go/install                          Install cli
  go/lint                             Lint code
  go/test                             Run tests
  go/vet                              Vet code
  helm/chart/build                    Build chart $CHART_NAME from $SOURCE_CHART_TPL
  helm/chart/build-all                Alias for helm/chart/build/all. Depricated.
  helm/chart/build/all                Build chart $CHART_NAME from $SOURCE_CHART_TPL for all available $SEMVERSIONS
  helm/chart/clean                    Clean chart packages
  helm/chart/create                   Create chart $CHART from starter scaffold
  helm/chart/promote/local            Promote $SOURCE_CHART_FILE to $TARGET_VERSION
  helm/chart/promote/remote           Promote $CHART_NAME from $SOURCE_VERSION to $TARGET_VERSION. ($SOURCE_CHART_REPO_ENDPOINT required)
  helm/chart/publish                  Alias for helm/chart/publish/all. WARNING: Eventually will became functional equal to helm/chart/publish/one
  helm/chart/publish/all              Publish chart $CHART_NAME to $TARGET_CHART_REPO_ENDPOINT
  helm/chart/publish/package          Publish chart $SOURCE_CHART_FILE to $REPO_GATEWAY_ENDPOINT
  helm/chart/starter/fetch            Fetch starter
  helm/chart/starter/remove           Remove starter
  helm/chart/starter/update           Update starter
  helm/delete/failed                  Delete all failed releases in a `NAMESPACE` subject to `FILTER`
  helm/delete/namespace               Delete all releases in a `NAMEPSACE` as well as the namespace
  helm/delete/namespace/empty         Delete `NAMESPACE` if there are no releases in it
  helmfile/install                    Install helmfile
  helm/install                        Install helm
  helm/repo/add                       Add $REPO_NAME from $REPO_ENDPOINT
  helm/repo/add-current               Add helm remote dev repos
  helm/repo/add-remote                Add helm remote repos
  helm/repo/build                     Build repo
  helm/repo/clean                     Clean helm repo
  helm/repo/fix-perms                 Fix repo filesystem permissions
  helm/repo/info                      Show repo info
  helm/repo/lint                      Lint charts
  helm/repo/update                    Update repo info
  helm/serve/index                    Build index for serve helm charts
  helm/toolbox/upsert                 Install or upgrade helm tiller 
  help                                Help screen
  help/all                            Display help for all targets
  help/short                          This help short screen
  jenkins/run-job-with-tag            Run a Jenkins Job with $(TAG)
  make/lint                           Lint all makefiles
  packages/delete                     Delete packages
  packages/install/%                  Install package (e.g. helm, helmfile, kubectl)
  packages/install                    Install packages 
  packages/reinstall/%                Reinstall package (e.g. helm, helmfile, kubectl)
  packages/reinstall                  Reinstall packages
  packages/uninstall/%                Uninstall package (e.g. helm, helmfile, kubectl)
  readme                              Alias for readme/build
  readme/build                        Create README.md by building it from README.yaml
  readme/init                         Create basic minimalistic .README.md template file
  readme/lint                         Verify the `README.md` is up to date
  semver/export                       Export semver vars
  slack/notify                        Send webhook notification to slack
  slack/notify/build                  Send notification to slack using "build" template
  slack/notify/deploy                 Send notification to slack using "deploy" template
  template/build                      Create $OUT file by building it from $IN template file
  template/deps                       Install dependencies
  terraform/get-modules               Ensure all modules can be fetched
  terraform/get-plugins               Ensure all plugins can be fetched
  terraform/install                   Install terraform
  terraform/lint                      Lint check Terraform
  terraform/upgrade-modules           Upgrade all terraform module sources
  terraform/validate                  Basic terraform sanity check
  travis/docker-login                 Login into docker hub
  travis/docker-tag-and-push          Tag & Push according Travis environment variables

```
## Extending `build-harness` with targets from another repo

It is possible to extend the `build-harness` with targets and entire modules of your own, without having to fork or modify `build-harness` itself.
This might be useful if, for example, you wanted to maintain some tooling that was specific to your environment that didn't have enough general applicability to be part of the main project.
This makes it so you don't necessarily need to fork `build-harness` itself - you can place a repo defined by the environment variable `BUILD_HARNESS_EXTENSIONS_PATH` (a filesystem peer of `build-harness` named `build-harness-extensions` by default) and populate it with tools in the same `Makefile` within `module` structure as `build-harness` has.
Modules will be combined and available with a unified `make` command. 



## Share the Love 

Like this project? Please give it a ★ on [our GitHub](https://github.com/sgcip/build-harness)! (it helps us **a lot**) 

Are you using this project or any of our other projects? Consider [leaving a testimonial][testimonial]. =)


## Related Projects

Check out these related projects.

- [Packages](https://github.com/cloudposse/packages) - Cloud Posse installer and distribution of native apps
- [Dev Harness](https://github.com/cloudposse/dev) - Cloud Posse Local Development Harness




## References

For additional context, refer to some of these links. 

- [Wikipedia - Test Harness](https://en.wikipedia.org/wiki/Test_harness) - The `build-harness` is similar in concept to a "Test Harness"


## Help

**Got a question?** We got answers. 

File a GitHub [issue](https://github.com/sgcip/build-harness/issues), send us an [email][email] or join our [Slack Community][slack].

## Contributing

### Bug Reports & Feature Requests

Please use the [issue tracker](https://github.com/sgcip/build-harness/issues) to report any bugs or file feature requests.

### Developing

If you are interested in being a contributor and want to get involved in developing this project or [help out](https://cpco.io/help-out) with our other projects, we would love to hear from you! Shoot us an [email][email].

In general, PRs are welcome. We follow the typical "fork-and-pull" Git workflow.

 1. **Fork** the repo on GitHub
 2. **Clone** the project to your own machine
 3. **Commit** changes to your own branch
 4. **Push** your work back up to your fork
 5. Submit a **Pull Request** so that we can review your changes

**NOTE:** Be sure to merge the latest changes from "upstream" before making a pull request!



## Copyrights

Copyright © 2017-2020 [Cloud Innovation Platform](https://portal.sgcip.com)





## License 

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) 

See [LICENSE](LICENSE) for full details.

    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      https://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.









## Trademarks

All other trademarks referenced herein are the property of their respective owners.

## About

[![CIP][logo]][cipcorpwebsite]  This project is maintained and funded by [CIP][cipcorpwebsite].

This Cloud Innovation Platform is built by passionate people located all around the world.
And because we ❤️ [Open Source Software][we_love_open_source], we decided to open source it.

You like that project? Please let us know by [leaving a testimonial][testimonial]!

Check out [our other projects][githubcorp], [follow us on twitter][twitter] or [apply for a job][jobs].


### Contributors

|  [![Erik Osterman][osterman_avatar]][osterman_homepage]<br/>[Erik Osterman][osterman_homepage] | [![Igor Rodionov][goruha_avatar]][goruha_homepage]<br/>[Igor Rodionov][goruha_homepage] | [![Andriy Knysh][aknysh_avatar]][aknysh_homepage]<br/>[Andriy Knysh][aknysh_homepage] | [![Sarkis][sarkis_avatar]][sarkis_homepage]<br/>[Sarkis][sarkis_homepage] | [![Alexander Babai][alebabai_avatar]][alebabai_homepage]<br/>[Alexander Babai][alebabai_homepage] | [![Jon Boulle][jonboulle_avatar]][jonboulle_homepage]<br/>[Jon Boulle][jonboulle_homepage] | [![Patrice Lachance][patlachance_avatar]][patlachance_homepage]<br/>[Patrice Lachance][patlachance_homepage] |
|---|---|---|---|---|---|---|

  [osterman_homepage]: https://github.com/osterman
  [osterman_avatar]: https://img.cloudposse.com/150x150/https://github.com/osterman.png
  [goruha_homepage]: https://github.com/goruha
  [goruha_avatar]: https://img.cloudposse.com/150x150/https://github.com/goruha.png
  [aknysh_homepage]: https://github.com/aknysh
  [aknysh_avatar]: https://img.cloudposse.com/150x150/https://github.com/aknysh.png
  [sarkis_homepage]: https://github.com/sarkis
  [sarkis_avatar]: https://img.cloudposse.com/150x150/https://github.com/sarkis.png
  [alebabai_homepage]: https://github.com/alebabai
  [alebabai_avatar]: https://img.cloudposse.com/150x150/https://github.com/alebabai.png
  [jonboulle_homepage]: https://github.com/jonboulle
  [jonboulle_avatar]: https://img.cloudposse.com/150x150/https://github.com/jonboulle.png
  [patlachance_homepage]: https://github.com/patlachance
  [patlachance_avatar]: https://img.cloudposse.com/150x150/https://github.com/patlachance.png

[![README Footer][readme_footer_img]][readme_footer_link]
[![Beacon][beacon]][website]

  [logo]: #
  [docs]: https://portal.sgcip.com/docs?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=docs
  [cipcorpwebsite]: https://portal.sgcip.com?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=website
  [githubcip]: https://github.com/sgcip/cip-core-platform?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=github
  [githubcorp]: https://github.com/sgcip/?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=github
  [jobs]: https://portal.sgcip.com/?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=jobs
  [slack]: https://portal.sgcip.com/slack?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=slack
  [linkedin]: https://www.linkedin.com/?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=linkedin
  [twitter]: https://twitter.com/sg_cip?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=twitter
  [testimonial]: https://portal.sgcip.com/leave-testimonial?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=testimonial
  [email]: https://portal.sgcip.com/contact?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=email
  [we_love_open_source]: https://portal.sgcip.com?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=we_love_open_source
  [readme_footer_img]: https://cloudposse.com/readme/footer/img
  [readme_footer_link]: https://cloudposse.com/readme/footer/link?utm_source=github&utm_medium=readme&utm_campaign=sgcip/build-harness&utm_content=readme_footer_link
  [share_twitter]: https://twitter.com/intent/tweet/?text=Build+Harness&url=https://github.com/sgcip/build-harness
  [share_linkedin]: https://www.linkedin.com/shareArticle?mini=true&title=Build+Harness&url=https://github.com/sgcip/build-harness
  [share_reddit]: https://reddit.com/submit/?url=https://github.com/sgcip/build-harness
  [share_facebook]: https://facebook.com/sharer/sharer.php?u=https://github.com/sgcip/build-harness
  [share_googleplus]: https://plus.google.com/share?url=https://github.com/sgcip/build-harness
  [share_email]: mailto:?subject=Build+Harness&body=https://github.com/sgcip/build-harness
  [beacon]: https://ga-beacon.sgcip.com/UA-167171211-1/sgcip/build-harness?pixel&cs=github&cm=readme&an=build-harness
