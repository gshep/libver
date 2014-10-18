Library Versioning 0
====================

Summary
-------

Given a version number MAJOR.MINOR.PATCH, increment the:

1. MAJOR version when you make source incompatible API changes or
    start new generation of the library,
1. MINOR version when you add functionality that preserves source
    compatibility (binary compatibility may be broken), and
1. PATCH version when you make bug fixes guaranteed both binary and source
    compatibilities are not broken.

Introduction
------------

See original introduction at http://semver.org

Library Versioning Specification (LibVer)
-----------------------------------------

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119](http://tools.ietf.org/html/rfc2119).

Definition of the terms 'binary compatibility' and 'source compatibility'
are given in
[KDE Policies](https://techbase.kde.org/Policies/Binary_Compatibility_Issues_With_C++#Definition).

1. Software using Library Versioning MUST declare a public API. This API
could be declared in the code itself or exist strictly in documentation.
However it is done, it should be precise and comprehensive.

1. A normal version number MUST take the form X.Y.Z where X, Y, and Z are
non-negative integers, and MUST NOT contain leading zeroes. X is the
major version, Y is the minor version, and Z is the patch version.
Each element MUST increase numerically. For instance: 1.9.0 -> 1.10.0 -> 1.11.0.

1. Once a versioned package has been released, the contents of that version
MUST NOT be modified. Any modifications MUST be released as a new version.

1. Patch version Z (x.y.Z) MUST be incremented if only backwards
compatible bug fixes are introduced. A bug fix is defined as an internal
change that fixes incorrect behavior.
If binary compatibility is broken by the patch then minor
version MUST be incremeted (see the next item). The current version (before
'fix') MUST remain the last in the x.y-branch. For example: there is
version 1.2.43 and a bug fix does not break binary compatibility so
new version is 1.2.44, i.e. 1.2.43 -> 1.2.44.
If a bug fix breakes binary compatibility then the new version MUST be 1.3.0
and after that 'fix' there MUST NOT exist 1.2.44.

1. Minor version Y (x.Y.z) MUST be incremented if new, backwards
compatible functionality is introduced to the public API. The changes MUST
NOT break source compatibility. The changes MAY break binary compatibility.
It MUST be incremented if any public API
functionality is marked as deprecated. It MAY be incremented if substantial
new functionality or improvements are introduced within the private code.
It MAY include patch level changes. Patch version MUST be reset to 0
when minor version is incremented.
If source compatibility is broken by the minor changes then major
version MUST be incremeted (see the next item). The current version (before
the changes) MUST remain the last in the x-branch.
For instance: 1.5.6 -> 1.6.0 --- source compatibility saved,
1.5.6 -> 2.0.0 --- source compatibility broken (1.5.7, 1.5.8 and so
MUST NOT exist).

1. Major version X (X.y.z) MUST be incremented if any
source incompatible changes are introduced to the public API. It MAY also
include minor and patch level changes. Patch and minor version MUST
be reset to 0 when major version is incremented. For instance:
2.6.73 -> 3.0.0.

1. Version MUST NOT contain any other information (build, date,
configurations, names, etc). Any such information MUST BE included
directly to the library as specific functions/methods and
duplicated in ChangeLogs/READMEs/etc.

FAQ
---

### How should I deal with revisions in the 0.y.z initial development phase?

The simplest thing to do is start your initial development release at 0.1.0
and then increment the minor version for each subsequent release.

### How do I know when to release 1.0.0?

If your software is being used in production, it should probably already be
1.0.0. If you have a stable API on which users have come to depend, you should
be 1.0.0. If you're worrying a lot about backwards compatibility, you should
probably already be 1.0.0.

### Doesn't this discourage rapid development and fast iteration?

Major version zero is all about rapid development. If you're changing the API
every day you should either still be in version 0.y.z or on a separate
development branch working on the next major version.

### If even the tiniest backwards incompatible changes to the public API require a major version bump, won't I end up at version 42.0.0 very rapidly?

This is a question of responsible development and foresight. Incompatible
changes should not be introduced lightly to software that has a lot of
dependent code. The cost that must be incurred to upgrade can be significant.
Having to bump major versions to release incompatible changes means you'll
think through the impact of your changes, and evaluate the cost/benefit ratio
involved.

### Documenting the entire public API is too much work!

It is your responsibility as a professional developer to properly document
software that is intended for use by others. Managing software complexity is a
hugely important part of keeping a project efficient, and that's hard to do if
nobody knows how to use your software, or what methods are safe to call. In
the long run, Semantic Versioning, and the insistence on a well defined public
API can keep everyone and everything running smoothly.

### What do I do if I accidentally release a backwards incompatible change as a minor version?

As soon as you realize that you've broken the Semantic Versioning spec, fix
the problem and release a new minor version that corrects the problem and
restores backwards compatibility. Even under this circumstance, it is
unacceptable to modify versioned releases. If it's appropriate,
document the offending version and inform your users of the problem so that
they are aware of the offending version.

### What should I do if I update my own dependencies without changing the public API?

That would be considered compatible since it does not affect the public API.
Software that explicitly depends on the same dependencies as your package
should have their own dependency specifications and the author will notice any
conflicts. Determining whether the change is a patch level or minor level
modification depends on whether you updated your dependencies in order to fix
a bug or introduce new functionality. I would usually expect additional code
for the latter instance, in which case it's obviously a minor level increment.

### What if I inadvertently alter the public API in a way that is not compliant with the version number change (i.e. the code incorrectly introduces a major breaking change in a patch release)

Use your best judgment. If you have a huge audience that will be drastically
impacted by changing the behavior back to what the public API intended, then
it may be best to perform a major version release, even though the fix could
strictly be considered a patch release. Remember, Semantic Versioning is all
about conveying meaning by how the version number changes. If these changes
are important to your users, use the version number to inform them.

### How should I handle deprecating functionality?

Deprecating existing functionality is a normal part of software development and
is often required to make forward progress. When you deprecate part of your
public API, you should do two things: (1) update your documentation to let
users know about the change, (2) issue a new minor release with the deprecation
in place. Before you completely remove the functionality in a new major release
there should be at least one minor release that contains the deprecation so
that users can smoothly transition to the new API.

### Is there any size limit on the version string?

No, but use good judgment. A 255 character version string is probably overkill,
for example. Also, specific systems may impose their own limits on the size of
the string.

About
-----

This work is based on [SemVer](http://semver.org).

License
-------

Creative Commons - CC BY 3.0
http://creativecommons.org/licenses/by/3.0/
