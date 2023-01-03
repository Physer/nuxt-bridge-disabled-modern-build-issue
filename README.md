# nuxt-bridge-disabled-modern-build-issue
A minimal reproduction repo of an issue with NuxtJS, bridge and the CLI

## Introduction
This repository shows an issue with the `--modern` flag for the Nuxt CLI.

When using Nuxt Bridge (`nuxt-edge` and `nuxt-bridge`) but `Nitro` is disabled as a build tool, the `--modern` flag is unable to resolve a Typescript import.

## Repository structure
There are 4 demo applications in this repository. Every application works with the regular build step or in dev mode. However, when using the `--modern` CLI flag with `nuxt` (read more), it doesn't work in one of the 4 applications: `nuxt-bridge-without-nuxi`.
| Application              | Nuxt version             | CLI tool | --modern flag works | Regular build works |
|--------------------------|--------------------------|----------|---------------------|---------------------|
| nuxt-v2                  | 2.15.8                   | nuxt     | :white_check_mark:  | :white_check_mark:  |
| nuxt-bridge              | 2.16.0-27720022.54e852f  | nuxi     | N/A                 | :white_check_mark:  |
| nuxt-bridge-without-nuxi | v2.16.0-27720022.54e852f | nuxt     | :x:                 | :white_check_mark:  |
| nuxt-v3                  | 3.0.0                    | nuxi     | N/A                 | :white_check_mark:  |

## Issue
The issue is as follows: when having Nuxt Bridge installed in a Nuxt V2 application but Nitro is disabled so we're using the Nuxt CLI, the `--modern` flag will break the build because it can't import the Typescript file that's used in the `~/pages/index.vue` file.

When this import is called with the file extension at the end (so `import data from '../externalFile'.ts`) it will work.

In a regular Nuxt V2 application, this does not present an issue.
