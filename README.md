# sf-chipps

[![NPM](https://img.shields.io/npm/v/sf-chipps.svg?label=sf-chipps)](https://www.npmjs.com/package/sf-chipps) [![Downloads/week](https://img.shields.io/npm/dw/sf-chipps.svg)](https://npmjs.org/package/sf-chipps) [![Known Vulnerabilities](https://snyk.io/test/github/ClayChipps/sf-chipps/badge.svg)](https://snyk.io/test/github/ClayChipps/sf-chipps) [![License: BSD-3-Clause](https://img.shields.io/badge/License-BSD_3--Clause-yellow.svg)](https://raw.githubusercontent.com/ClayChipps/sf-chipps/main/LICENSE.txt)

## Install

```bash
sf plugins install sf-chipps
```

## Issues

Please report any issues at https://github.com/ClayChipps/sf-chipps/issues

## Commands

<!-- commands -->
* [`sf chipps package dependencies install`](#sf-chipps-package-dependencies-install)
* [`sf chipps package version cleanup`](#sf-chipps-package-version-cleanup)

## `sf chipps package dependencies install`

Install package dependencies for a Salesforce project.

```
USAGE
  $ sf chipps package dependencies install -o <value> [--json] [-a all|package] [--api-version <value>] [-z <value>] [-i All|Delta] [-k
    <value>] [-r] [-b <value>] [-s AllUsers|AdminsOnly] [-v <value>] [-t DeprecateOnly|Mixed|Delete] [-w <value>]

FLAGS
  -a, --apex-compile=<option>        Compile all Apex in the org and package, or only Apex in the package; unlocked
                                     packages only.
                                     <options: all|package>
  -b, --publish-wait=<value>         [default: [object Object]] Maximum number of minutes to wait for the Subscriber
                                     Package Version ID to become available in the target org before canceling the
                                     install request.
  -i, --install-type=<option>        [default: Delta] Install all packages or only deltas.
                                     <options: All|Delta>
  -k, --installation-key=<value>...  Installation key for key-protected packages
  -o, --target-org=<value>           (required) Username or alias of the target org. Not required if the `target-org`
                                     configuration variable is already set.
  -r, --no-prompt                    Don't prompt for confirmation.
  -s, --security-type=<option>       [default: AdminsOnly] Security access type for the installed package. (deprecation
                                     notice: The default --security-type value will change from AllUsers to AdminsOnly
                                     in v47.0 or later.)
                                     <options: AllUsers|AdminsOnly>
  -t, --upgrade-type=<option>        [default: Mixed] Upgrade type for the package installation; available only for
                                     unlocked packages.
                                     <options: DeprecateOnly|Mixed|Delete>
  -v, --target-dev-hub=<value>       Username or alias of the Dev Hub org.
  -w, --wait=<value>                 [default: [object Object]] Number of minutes to wait for installation status.
  -z, --branch=<value>               Package branch to consider when specifiyng a Package/VersionNumber combination
      --api-version=<value>          Override the api version used for api requests made by this command

GLOBAL FLAGS
  --json  Format output as json.

DESCRIPTION
  Install package dependencies for a Salesforce project.

  Installs all specified package dependencies in a Salesforce DX project using the sfdx-project.json definition.

EXAMPLES
  $ sf chipps package dependencies install --target-org myTargetOrg --target-dev-hub myTargetDevHub

  $ sf chipps package dependencies install --target-org myTargetOrg --target-dev-hub myTargetDevHub --installation-key "MyPackage1Alias:MyPackage1Key"

  $ sf chipps package dependencies install --target-org myTargetOrg --target-dev-hub myTargetDevHub --installation-key "MyPackage1Alias:MyPackage1Key" --installation-key "MyPackage2Alias:MyPackage2Key"

FLAG DESCRIPTIONS
  -a, --apex-compile=all|package

    Compile all Apex in the org and package, or only Apex in the package; unlocked packages only.

    Applies to unlocked packages only. Specifies whether to compile all Apex in the org and package, or only the Apex in
    the package.

    For package installs into production orgs, or any org that has Apex Compile on Deploy enabled, the platform compiles
    all Apex in the org after the package install or upgrade operation completes.

    This approach assures that package installs and upgrades don’t impact the performance of an org, and is done even if
    --apex-compile package is specified.

  -i, --install-type=All|Delta  Install all packages or only deltas.

    If 'All' is specified, then all packages specified in package dependencies are installed, regardless of if the
    version already is installed in the org. If 'Delta' is specified, then only packages that differ from what is
    installed in the org will be installed.

  -k, --installation-key=<value>...  Installation key for key-protected packages

    Installation key for key-protected packages in the key:value format of SubscriberPackageVersionId:Key

  -r, --no-prompt  Don't prompt for confirmation.

    Allows the following without an explicit confirmation response: 1) Remote Site Settings and Content Security Policy
    websites to send or receive data, and 2) --upgrade-type Delete to proceed.

  -t, --upgrade-type=DeprecateOnly|Mixed|Delete

    Upgrade type for the package installation; available only for unlocked packages.

    For package upgrades, specifies whether to mark all removed components as deprecated (DeprecateOnly), to delete
    removed components that can be safely deleted and deprecate the others (Mixed), or to delete all removed components,
    except for custom objects and custom fields, that don't have dependencies (Delete). The default is Mixed. Can
    specify DeprecateOnly or Delete only for unlocked package upgrades.

  -z, --branch=<value>  Package branch to consider when specifiyng a Package/VersionNumber combination

    For dependencies specified by Package/VersionNumber combination, you can specify the branch group of builds to work
    from by entering the branch build name. If not specified, the builds from NULL branch will be considered.
```

_See code: [sf-chipps-package](https://github.com/ClayChipps/sf-chipps-package/blob/1.2.7/src/commands/chipps/package/dependencies/install.ts)_

## `sf chipps package version cleanup`

Cleanup package versions.

```
USAGE
  $ sf chipps package version cleanup -s <value> -p <value> -v <value> [--json] [--api-version <value>]

FLAGS
  -p, --package=<value>         (required) Package Id
  -s, --matcher=<value>         (required) MAJOR.MINOR.PATCH
  -v, --target-dev-hub=<value>  (required) Username or alias of the Dev Hub org. Not required if the `target-dev-hub`
                                configuration variable is already set.
      --api-version=<value>     Override the api version used for api requests made by this command

GLOBAL FLAGS
  --json  Format output as json.

DESCRIPTION
  Cleanup package versions.

  Delete package versions for a given package provided a MAJOR.MINOR.PATCH matcher. Does not delete released pacakge
  versions.

EXAMPLES
  $ sf chipps package version cleanup --package 0Hoxx00000000CqCAI --matcher 2.10.0 --target-dev-hub myDevHub

FLAG DESCRIPTIONS
  -p, --package=<value>  Package Id

    The 0Ht Package Id that you wish to cleanup versions for.

  -s, --matcher=<value>  MAJOR.MINOR.PATCH

    The MAJOR.MINOR.PATCH matcher that should be used to find package versions to delete.
```

_See code: [sf-chipps-package](https://github.com/ClayChipps/sf-chipps-package/blob/1.2.7/src/commands/chipps/package/version/cleanup.ts)_
<!-- commandsstop -->
