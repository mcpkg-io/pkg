# pkg 📦

<a href="https://packagist.org/packages/mcpkg-io/pkg"><img src="https://img.shields.io/packagist/dt/mcpkg-io/pkg" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/mcpkg-io/pkg"><img src="https://img.shields.io/packagist/v/mcpkg-io/pkg" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/mcpkg-io/pkg"><img src="https://img.shields.io/packagist/l/mcpkg-io/pkg" alt="License"></a>
<a href="https://discord.gg/qsxVMNg"><img src="https://discordapp.com/api/guilds/552952675369484301/embed.png?style=shield" alt="Discord"></a>

A Package Manager for Minecraft

## Introduction 🦄

With Package, also known as `pkg`, you can easily install and update servers, plugins, maps and even complete pre-configured servers just by using the `pkg` command. It does not require any technical knowledge.

<p align="center">
  <img src="demo.gif">
</p>

Built to be jusT cOol 😎!

> If you think so, support us with a `star` and a `follow` 😘

## Usage 🎉

After installing pkg, you can easily set up your first Minecraft Server by using the following command:

    pkg create-server pkg/paper my-server

This command will use `pkg/paper` as template and download PaperMC using the latest version within seconds.

## Install on Linux 🚀

This won't take long...

    curl -sfL https://get.mcpkg.io | sh -

Tip: Checkout our [GitHub Action](https://github.com/mcpkg-io/pkg-action) for CI/CD.

## Install on Windows 🛸

On Windows, it's a little bit more work to get pkg's install requirements installed. You can use our Windows Installation Guide, if you're already installed Composer successful, you can run:

    composer global require mcpkg-io/pkg

## Finding Packages 🔍

> At the moment, we're quite new, so there is not much content published using pkg, but you can increase this by making plugin developers aware of this project.

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

## Getting Started as Package Developer 🧑‍💻

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

### Exact Version Constraint

You can specify the exact version of a package. This will tell Package to
install this version and this version only. If other dependencies require
a different version, the solver will ultimately fail and abort any install
or update procedures.

Example: `1.0.2`

### Version Range

By using comparison operators you can specify ranges of valid versions. Valid
operators are `>`, `>=`, `<`, `<=`, `!=`.

You can define multiple ranges. Ranges separated by a space (<code>&nbsp;</code>)
or comma (`,`) will be treated as a **logical AND**. A double pipe (`||`)
will be treated as a **logical OR**. AND has higher precedence than OR.

> **Note:** Be careful when using unbounded ranges as you might end up
> unexpectedly installing versions that break backwards compatibility.
> Consider using the [caret](#caret-version-range-) operator instead for safety.

Examples:

* `>=1.0`
* `>=1.0 <2.0`
* `>=1.0 <1.1 || >=1.2`

### Hyphenated Version Range (` - `)

Inclusive set of versions. Partial versions on the right include are completed
with a wildcard. For example `1.0 - 2.0` is equivalent to `>=1.0.0 <2.1` as the
`2.0` becomes `2.0.*`. On the other hand `1.0.0 - 2.1.0` is equivalent to
`>=1.0.0 <=2.1.0`.

Example: `1.0 - 2.0`

### Wildcard Version Range (`.*`)

You can specify a pattern with a `*` wildcard. `1.0.*` is the equivalent of
`>=1.0 <1.1`.

Example: `1.0.*`

## Next Significant Release Operators

### Tilde Version Range (`~`)

The `~` operator is best explained by example: `~1.2` is equivalent to
`>=1.2 <2.0.0`, while `~1.2.3` is equivalent to `>=1.2.3 <1.3.0`. As you can see
it is mostly useful for projects respecting [semantic
versioning](https://semver.org/). A common usage would be to mark the minimum
minor version you depend on, like `~1.2` (which allows anything up to, but not
including, 2.0). Since in theory there should be no backwards compatibility
breaks until 2.0, that works well. Another way of looking at it is that using
`~` specifies a minimum version, but allows the last digit specified to go up.

Example: `~1.2`

> **Note:** Although `2.0-beta.1` is strictly before `2.0`, a version constraint
> like `~1.2` would not install it. As said above `~1.2` only means the `.2`
> can change but the `1.` part is fixed.

> **Note:** The `~` operator has an exception on its behavior for the major
> release number. This means for example that `~1` is the same as `~1.0` as
> it will not allow the major number to increase trying to keep backwards
> compatibility.

### Caret Version Range (`^`)

The `^` operator behaves very similarly, but it sticks closer to semantic
versioning, and will always allow non-breaking updates. For example `^1.2.3`
is equivalent to `>=1.2.3 <2.0.0` as none of the releases until 2.0 should
break backwards compatibility. For pre-1.0 versions it also acts with safety
in mind and treats `^0.3` as `>=0.3.0 <0.4.0`.

This is the recommended operator for maximum interoperability when writing
library code.

Example: `^1.2.3`

## Private Packages 😶‍🌫️

Currently in private-beta, we're experimenting with private packages. Private Packages allows you to distribute packages in private environments, like huge server networks.

There is no special setup required to create private packages. The permission management is done within the package settings page.

## Contributing 🧙

If you want to contribute to this project, please feel free to create any pull request, but please consider reading our contribution guidelines first.

## Server Integrations 🔌

Currently we're still busy creating the core cli application, including the website, but we've already planned an plugin integration for Minecraft servers bringing `/pkg` available as in-game command.

The plugin itself wraps the cli command and bringing some additional quality of life tools, like in-game plugin reloading.

## License 🧑‍⚖️

Package, also known as pkg, and all content on this repository are released under the [MIT license](LICENSE).

To explain version constraints, we used the docs from [Composer](https://getcomposer.org/doc/articles/versions.md).
