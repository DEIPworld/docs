---
description: Read on for a brief introduction to DEIP's low-code Constructor.
---

# Low-code Constructor

The low-code Constructor is a free, open-source tool that helps developers build their applications \(i.e. Portals\) in the DEIP Network. This tool requires basic programming skills because you build Portals by assembling ready-made software modules.

We designed a set of ready-to-use software modules, consisting of Java Script packages to build frontend applications and Portals. The modules allow you to avoid immersing yourself in the low-level technical features of the technology and make it possible to launch a quality project quickly and safely. 

## Building guide

Check out our video guide below to get started 📺

{% embed url="https://youtu.be/C5VwmWefSbI" caption="DEIP low-code Constructor" %}

## Modules

The DEIP-modules repository consists of Java Script packages designed to build frontend applications and Portals. Modules allow you to connect to services to interact with DEIP infrastructure and are implemented using the Vue framework and Vuetify components library.

## Quickstart

Go to our [Modules GitHub repository](https://github.com/DEIPworld/deip-modules) to get started 🛠️

We use [Lerna](https://github.com/lerna/lerna) for managing our packages.

### Prepare repo for work

We recommend you install Lerna globally:

```text
npm install -g lerna
```

```text
npm install && npm run bootstrap
```

#### Basic: Add module \(internal/external\)

Check [docs](https://github.com/lerna/lerna) for all commands.

For all packages

```text
lerna add [module name]
```

Specified package

```text
lerna add [module name] --scope=[target]
```

#### Publish

Publishing is only allowed from develop and master branches. Branches must be clean and up to date.

```text
npm run publish
```

