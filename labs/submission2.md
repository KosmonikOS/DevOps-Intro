# Lab 2 Submission

## Task 1

### Finding Object Hashes

First, I retrieved the commit hash and inspected the commit object to find the tree and blob hashes (I've blurred SSH key in the screenshot):

![Finding object hashes](img/hashes.png)


### Inspecting Git Objects

![Inspecting blob, tree, and commit objects](img/inspect.png)


A blob (Binary Large Object) stores the raw content of a file without any metadata like filename or permissions. It represents a snapshot of file contents at a specific point in time.

A tree object represents a directory snapshot. It contains entries with file mode, object type (blob or tree), SHA-1 hash, and filename — essentially mapping names to blobs (files) or other trees (subdirectories).

A commit object contains a pointer to the root tree (project snapshot), parent commit(s), author/committer metadata with timestamps, an optional GPG/SSH signature, and the commit message.

### Analysis: How Git Stores Data

Git uses a content-addressable filesystem based on SHA-1 hashes. The storage model consists of three core object types:

1. Blobs — store file contents only (no filenames)
2. Trees — store directory structure, mapping names to blobs and subtrees
3. Commits — store metadata and point to a tree representing the project state

This design enables:
- Deduplication: Identical file contents share the same blob hash
- Integrity: Any change produces a completely different hash
- Efficient storage: Objects are compressed and stored in `.git/objects/`

