3D Library Versioning 1
=======================

Summary
-------

Given a version number MAJOR.MINOR.PATCH, increment the:

1. MAJOR version when you make source incompatible API changes,
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
the version 1.2.43 and a bug fix does not break binary compatibility so
the new version is 1.2.44, i.e. 1.2.43 -> 1.2.44.
If a bug fix breakes binary compatibility then the new version MUST be 1.3.0
and after that 'fix' there MUST NOT exist 1.2.44, 1.2.45 and so on.

1. Minor version Y (x.Y.z) MUST be incremented if new
functionality is introduced to the public API. The changes MUST
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
1.5.6 -> 2.0.0 --- source compatibility broken (1.5.7, 1.5.8 and so on
MUST NOT exist).

1. Major version X (X.y.z) MUST be incremented if any
source incompatible changes are introduced to the public API. It MAY also
include minor and patch level changes. Patch and minor version MUST
be reset to 0 when major version is incremented. For instance:
2.6.73 -> 3.0.0.

1. Version MUST NOT contain any other information (build, date,
configurations, names, etc). Any such information MUST BE provided
directly by the library as specific interface(s) and
documented in ChangeLogs/READMEs/etc.

FAQ
---

### What does '3D' in the name mean?

It means three digits or decimals. Actually title of
the guide should be read as 'how to version a library
with three digits/decimals?'.

### Therefore may there exist '2D', '4D', ... patterns of versioning?

To tell the truth, yes.

But at first let's consider versioning with one or two digits.
For shared libraries of compiled languages there are at least
two the most important issues: API (source compatibility) and
ABI (binary compatibility). To reflect changes
in API/ABI of a library two digits are required. Also
a developer needs to version bugfixes of a library.
Therefore, three decimals are the minimum possible count of
decimals to version a library.

TODO about '4d' and so  on.

See also original FAQ at http://semver.org

About
-----

This work is based on [SemVer](http://semver.org).

License
-------

Creative Commons - CC BY 3.0
http://creativecommons.org/licenses/by/3.0/
