# Patches for Strapi security issue 2212 (Users-Permissions-Template)

## Introduction

As you [may be aware](https://github.com/strapi/strapi/releases/tag/v4.5.6), Strapi was made aware of a critical security vulnerability that was patched in v4.5.6. If you're looking at this guide, it means you are on a version of Strapi less than v4.5.6 and are trying to apply [this fix](https://github.com/strapi/strapi/pull/15385), before you upgrade your Strapi app. This guide is split into two parts: patching your app with your own files, and patching your application with patch files obtained from the Strapi team.

## Prerequisites

For this guide, it's imperative that you are familiar (not an expert) with [patch-package](https://github.com/ds300/patch-package). Ideally, your only use of patch-package will you require you to apply the patch using a single command.

## Setting up your project

This zip contains various patch versions for the latest "patch version" for the latest minor releases. You should only pick the proper patch folder for the version you are on, if your version is not listed we ask that you please upgrade to the closest version. 

For example:

- If you are currently on v4.0.7, you should upgrade your application to v4.0.8 BEFORE you apply the patches
- If you are currently on a v3 version below v3.6.11, you should upgrade your application to v3.6.11 BEFORE you apply the patches

For update guides see the following documentation:

- For v4 you can use the [following documentation](https://docs.strapi.io/developer-docs/latest/update-migration-guides/update-version.html)
- For v3 you can use the [following documentation](https://docs-v3.strapi.io/developer-docs/latest/update-migration-guides/update-version.html)

### Required packages

1. You will need the following packages installed in your application: `patch-package` and `postinstall-postinstall`
   1. For NPM: `npm install patch-package postinstall-postinstall`
   2. For Yarn: `yarn add patch-package postinstall-postinstall`
2. Edit your `package.json` file to add the patch-package script to your `scripts`.

```json
// Path: `./package.json`

{
  "name": "your-strapi-app",
  // ...
  "scripts": {
    // ...
    "postinstall": "patch-package"
  },
  // ...
}
```

### Using the patch files

After choosing your desired version, copy and paste the patches folder into your application at the root of the Strapi app (if you are using a monorepo)

#### Sample V4 app structure

```
├── config
├── database
├── node_modules
├── patches
│   ├── @strapi+plugin-email+4.0.8.patch
│   ├── @strapi+plugin-users-permissions+4.0.8.patch
│   └── @strapi+utils+4.0.8.patch
├── public
├── src
├── .gitignore
└── package.json
```

#### Sample V3 app structure

```
├── api
├── config
├── extensions
├── node_modules
├── patches
│   ├── strapi-plugin-email+3.6.11.patch
│   └── strapi-plugin-users-permissions+3.6.11.patch
├── public
├── .gitignore
└── package.json
```

### Apply the patch

Once you have your package.json configured and the patches copied into your app; in order to apply the patches you will need to reinstall your node modules:

- For NPM: `npm install -f`
- For Yarn: `yarn install -f`

Patch-package should notify after you install the modules that it has applied the patches, see the following example response below:

```bash
user@hostname:~/yourApp$ yarn install -f
yarn install v1.22.19
[1/5] Validating package.json...
[2/5] Resolving packages...
success Already up-to-date.
$ patch-package
patch-package 6.5.1
Applying patches...
strapi-plugin-email@3.6.11 ✔
strapi-plugin-users-permissions@3.6.11 ✔
Done in 0.80s.
```
