Version: 1.0.1
==============

* Fixed php warning in class `PHPExecutor` due to trait being used twice


Version: 1.0
============

This release is aligned with kaliop/ezmigrationbundle rel. 6.3.1 / tanoconsulting/ezmigrationbundle2 rel. 1.0.1

* New: migration step `migration_definition/include`. This allows one migration to basically include another, the same
  way it is possible to do that in php.

  It is useful for scenarios such as fe. creating a library of reusable migrations, which can be run multiple times with
  different target contents every time. This is often achieved by copy-pasting the same migration logic many times.
  As an alternative it is now possible to create a "library" migration, driven by references, and store it only once,
  in a separate folder, then create many "specific execution" migrations which set up values for the required references
  and include the library migration's definition.

  Please note that migrations which rely on external resources, such as in this case would be the included migration, go
  against the principle of migrations being immutable for ease of replay and analysis.

  Ex:

        -
            type: migration_definition
            mode: include
            file: a_path

* New: implemented all changes which were implemented in the kaliop/ezmigrationbundle version of this tool between
  releases 5.15.1 and 6.2.1. The list is too long to be copied verbatim here; it can be found online at
  https://github.com/kaliop-uk/ezmigrationbundle/blob/main/WHATSNEW.md

* Fixed: when generating contentType migrations, do export the `is-thumbnail` attribute for Content Type Fields, and
  the Content Type's `default_always_available`, `default_sort_order` and `default_sort_field`

* Fixed: php warning when generating `Role` migrations for roles with policy limitations

* Improved: when executing migrations with the `set-reference` cli option, the injected references will be saved in the
  migration status

* Improved: add to the test matrix running on GitHub Ibexa-OSS version 4.3

* BC change (for developers extending the bundle): method `MigrateCommand::executeMigrationInProcess` changed its signature

* BC change (for developers extending the bundle): `Migrationservice` methods `executeMigration`, `executeMigrationInner`
  and `resumeMigration` now have a different signature. `Migrationservice::migrationContextFromParameters` has been dropped


Version 1.0-alpha1
==================

Initial release - forked from tanoconsulting/ezmigrationbundle2 ver. 1.0 alpha 3, merging wizhippo/ibexa-migration-bundle

*Changes compared to tanoconsulting/ezmigrationbundle2 ver. 1.0 alpha 3:*

* Fixed: in rare circumstances (having two siteaccesses configured with the same repo and root node, but different languages),
  the TagMatcher could use the wrong language when matching by tag keyword

* BC change (for developers extending the bundle): class `TagMatcher` changed its constructor signature. the same applies
  to service `ez_migration_bundle.tag_matcher`

*Explanation of the 'aplha' tag:*

1. the codebase itself is fairly _stable_ and _complete_, as it is a fork of a project which had over 75 releases already
2. on the other hand, given that the underlying cms framework has evolved a lot, there might be bugs due to API changes
3. also, not all features of the underlying cms framework are fully supported

*BC with eZMigrationBundle:*

See [ezmigrationbundle_to_ezmigrationbundle2.md](Resources/doc/Upgrading/ezmigrationbundle_to_ezmigrationbundle2.md)
for all API changes if you are used to eZMigrationBundle 1.
