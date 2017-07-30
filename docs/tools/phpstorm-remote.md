!!!warning # WORK IN PROGRESS - based on phpstorm.md but for remote debugging/testing.

# Using PhpStorm for CiviCRM Development

[PhpStorm](https://www.jetbrains.com/phpstorm) is a commercial IDE which is popular among CiviCRM developers.


## General project setup

* Use the root directory of your CMS as your project root (otherwise in-app debugging won't work)
* You can speed up PhpStorm's indexing process by taking the following steps to ignore most files:
    1. Settings > Directories
    1. Mark all directories as "Excluded"
    1. Drill down to find the "civicrm" folder and mark it as "Sources"

## Code style setup

Create the 'CiviCRM' code styling preference:

1. Open you current project's properties: File > Settings
1. Create the CiviCRM code styling preference: Code Style > Manage > Save as, then indicate 'CiviCRM'
1. In the 'Code style' sub-menu, select 'PHP', then 'Set from ...' at the far right, Predefined Style > Drupal (this sets options across all tabs of the dialog)
1. In the 'Code style' sub-menu, select 'Javascript', then 'Set from ...' at the far right, PHP (this replicates all PHP settings to the Javascript section)
1. Click 'Apply' at the bottom of the screen

That's it. You can now use this code style on all future CiviCRM-related projects. If you are only developing for CiviCRM, you can also copy this style to the 'Default' style.

## XDebug integration

TODO

## Running automated tests from within PhpStorm {:#testing}

!!! note
    These instructions assume you already have a working instance of CiviCRM running locally with [buildkit](/tools/buildkit).

From the `Run > Edit Configurations` menu add a new PHPUnit configuration.

Check "Use alternative configuration file" and choose `phpunit.xml.dist` in your
CiviCRM root directory.

Expand "Environment variables" and add the following two:

- `TEST_DB_DSN`: Use the DSN to connect to your test database. It is displayed
on completion of civibuild. You should also be able to find it by running
`cv vars:show`.
- `CIVICRM_UF`: Use "UnitTests" unless you're running WebTests or End-to-end
tests.

### Adding external libraries

It can be frustrating when writing tests the PHPStorm complains about missing
classes or undefined methods. This happens because PHPUnit is not included in
the CiviCRM codebase.

To remedy this you can add an external content root. You'll need to clone the
[phpunit] library locally. Then from that directory check out the latest supported
version of phpunit (4.x right now).

After that you just add the directory to your project include paths by
[following the instructions on the Jetbrains site][phpstorm-include-paths].

[phpstorm-include-paths]: https://www.jetbrains.com/help/phpstorm/configuring-include-paths.html
[phpunit]: https://github.com/sebastianbergmann/phpunit


## Running automated tests remotely from within PhpStorm {:#testing}
!!! note
    These instructions assume you already have a working instance of CiviCRM running locally with [buildkit](/tools/buildkit).

From the `Run > Edit Configurations` menu add a new PHPUnit configuration.
