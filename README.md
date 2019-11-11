CarthageDirectoryTraversal
==========================

The purpose of this repository is to point out Carthage's weird behavior that happens when a dependency contains a local path.

## Overview

When Cartfile contains `git ".."` as a local dependency, Carthage clones it in the wrong directory.
Usually Carthage clones and extracts a dependency in the directory named `Carthage/` but in that case, the dependency is extracted into `Carthage/../`, the parent directory of the correct path.

## Steps to reproduce

```
git clone https://github.com/manicmaniac/CarthageDirectoryTraversal.git
cd CarthageDirectoryTraversal/Carthage
carthage checkout
```

`carthage checkout` will be successfully finished but when you run `ls Carthage/Checkouts` there's nothing.
But when you run `ls Carthage/` instead, you can see the cloned repository `CarthageDirectoryTraversal` in the wrong place.
