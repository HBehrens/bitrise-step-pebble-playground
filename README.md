Sample project to test the CI-service [Bitrise](https://www.bitrise.io) with the
[Pebble build step](https://github.com/HBehrens/bitrise-step-pebble-build]).

Use this `workflow.yml` to build it

```
format_version: 1.2.0
default_step_lib_source: https://github.com/bitrise-io/bitrise-steplib.git
title: Bitrise example for Pebble
description: |-
  To use this workflow, import you Pebble project,
  add a custom workflow, and
  replace its yml with the content of this file
trigger_map:
- pattern: "*"
  is_pull_request_allowed: true
  workflow: build
workflows:
  build:
    description: |-
      You can use this workflow by running: bitrise run test
      Or by triggering: bitrise trigger test
      If you use trigger, you can trigger it with any pattern
        which starts with 'test', like: bitrise trigger test-1
        or: bitrise trigger test/1
      You can define the mapping between trigger patterns and
        workflows in the 'trigger_map' section.
    steps:
    - git-clone@3.2.0: {}
    - git::https://github.com/HBehrens/bitrise-step-pebble-build.git@master:
        title: Pebble build
        inputs:
        - sdk_without_emulator: 'yes'
        - sdk_without_freetype: 'yes'
        - sdk_without_node: 'yes'
        - sdk_accept_legalese: 'yes'
```
