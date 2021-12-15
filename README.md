# pkg 📦

A Package Manager for Minecraft

## Introduction

With Package, also known as `pkg`, you can easily install and update servers, plugins, maps and even complete pre-configured servers just by using the `pkg` command. It does not require any technical knowledge.

## Usage 🎉

After installing pkg, you can easily set up your first Minecraft Server by using the following command:

pkg create-server pkg/paper my-server

This command will use `pkg/paper` as template and download PaperMC using the latest version within seconds.

## Install on Linux 🚀

This won't take long...

    curl -sfL https://get.mcpkg.io | sh -

Tip: Checkout our [GitHub Action](https://github.com/mcpkg-io/pkg-action) for CI/CD.

## Install on Windows 🛸

On Windows, it's a little bit more work to get pkg's imstall requirements installed. You can use our Windows Installation Guide, if you're already installed Composer successful, you can run:

    composer global require mcpkg-io/pkg

## Finding Packages 🔍

> At the moment, we're quite new, so there are not much content published using pkg, but you can increase this by making plugin developers aware of this project.

You will the most of packages, which are available for pkg, at our official [mcpkg.io](https://www.mcpkg.io/) website, or by using the instructions from the package vendor.

## Require Packages 📦

After you found a package you like, you can install it by using the `require` command, run:

    pkg require example/hello-world

Or by using a specific version:

    pkg require example/hello-world:^1.0

Using specific versions helps you to prevent unintentional breaking changes. By default, pkg will use `^`,  it sticks closer to semantic versioning and will always allow non-breaking updates.

You can read more about writing constraints in our Version Constraints section.

## Terminology 🧑‍🎓

**Package**: A 3rd-party dependency which can be required, like servers, plugins, maps or metapackages.

**Metapackage**: A predefined pkg.json, which mostly already contains the server, some plugins and maps.

**Vendor**: A person or organization which publish packages.

**Semver**: Semantic Versioning is a versioning scheme for using meaningful version numbers. It's a commonly used method by software developers.

## Getting Started as Package Developer

It's quite simple to get you package published and available for pkg, you just need to create a free account to register your vendor name. A vendor name is used to distinguish packages between multiple developers, for example.

To sign up or sign in with your developer account, just run:

    pkg login

This will open a new browser tab where you can authenticate. After successful login, a access token will be automatically stored on your local computer. With this token, you can easily publish your packages to mcpkg.io.

Now you need to create a new pkg.json file, which tells pkg, what's your package is about. This can be done by using the following command:

    pkg init

The `init` command will guide you through the creation process by asking simple question.

After successful creation, you can upload your package by using the `publish` command. It will upload the complete current working directory (or the given directory). Be careful not to publish any secrets.

    pkg publish

Finally, you can `require` your package. Tell the world about your release!

## Version Constraints 💪

Now since you having a rough understanding about using pkg, let's talk about writing version constraints.

Version constraints helps you to automatically select the right package version. They will be automatically resolved during an `require` or `update`.

TBD

## Private Packages 😶‍🌫️

Currently in private-beta, we're experimenting with private packages. Private Packages allows you to distribute packages in private environments, like huge server networks.

There is no special setup required to create private packages. The permission management is done within the package settings page.


