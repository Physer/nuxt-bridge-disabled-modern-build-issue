# nuxt-bridge-disabled-modern-build-issue
A minimal reproduction repo of an issue with NuxtJS, bridge and the CLI

## Introduction
This repository shows an issue with the `--modern` flag for the Nuxt CLI.

When using Nuxt Bridge (`nuxt-edge` and `nuxt-bridge`) but `Nitro` is disabled as a build tool, the `--modern` flag is unable to resolve a Typescript import.

## Repository structure
There are 4 demo applications in this repository. Every application works with the regular build step or in dev mode. However, when using the `--modern` CLI flag with `nuxt` ([read more](https://nuxtjs.org/docs/configuration-glossary/configuration-modern#the-modern-property)), it doesn't work in one of the 4 applications: `nuxt-bridge-without-nuxi`.
| Application              | Nuxt version             | CLI tool | --modern flag works | Regular build works |
|--------------------------|--------------------------|----------|---------------------|---------------------|
| nuxt-v2                  | 2.15.8                   | nuxt     | :white_check_mark:  | :white_check_mark:  |
| nuxt-bridge              | 2.16.0-27720022.54e852f  | nuxi     | N/A                 | :white_check_mark:  |
| nuxt-bridge-without-nuxi | 2.16.0-27720022.54e852f  | nuxt     | :x:                 | :white_check_mark:  |
| nuxt-v3                  | 3.0.0                    | nuxi     | N/A                 | :white_check_mark:  |

## Project structure
Every application has the same structure.
There is a Typescript file: `~/externalFile.ts`. This is an object that gets exported.

On the Index page (`~/pages/index.vue`) this file gets imported and the object gets rendered on the page through the `data` hook.

## Issue
The issue is as follows: when having Nuxt Bridge installed in a Nuxt V2 application but Nitro is disabled so we're using the Nuxt CLI, the `--modern` flag will break the build because it can't import the Typescript file that's used in the `~/pages/index.vue` file.

When this import is called with the file extension at the end (so `import data from '../externalFile'.ts`) it will work.

In a regular Nuxt V2 application, this does not present an issue.

### Reproducing the issue
In order to see the issue, first take a look at the working version.

In the `nuxt-v2` application run the following commands (in the `~/nuxt-v2` folder):
* yarn
* yarn build-modern
* yarn start

Everything works as expected and when you navigate to `http://localhost:3000` you can see the Typescript file's output on screen.

Now go to the `~/nuxt-bridge-without-nuxi` folder and run the same commands.

This will fail due to being unable to locate the Typescript file.

## Nuxt Bridge without Nitro configuration
The failing application has a peculiar configuration.
Nuxt Bridge has been installed, yet `nitro` has been disabled in the `nuxt.config.ts`. So `nuxi` can't be used.