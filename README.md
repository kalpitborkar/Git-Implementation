# PyGit
PyGit is implementation of the [Git version control system](https://git-scm.com/) from scratch, written purely in Python.

PyGit implements all the fundamental features of git:
  - `add`
  - `cat-file`
  - `checkout`
  - `commit`
  - `hash-object`
  - `init`
  - `log`
  - `ls-tree`
  - `merge`
  - `rebase`
  - `rev-parse`
  - `rm`
  - `show-ref`
  - `tag`

# PyGit structure
- `GitRepository`:
  - Object representing a git repository.
  - `GitRepository` consists of two things: 
    - `worktree` - a “work tree”, where the files meant to be in version control live.
    - `gitdir` -  “git directory”, where Git stores its own data.

- `GitObject`:
  - Objects are of multiple types, and they all share the same storage/retrieval mechanism and the same general header format.
  - `GitOject` is a generic object with two unimplemented methods:
    - `serialize()`
    - `deserialize()`

- `GitBlob`:
  - Blobs are user content: every file you put in git is stored as a blob.
  - The `serialize` and `deserialize` functions store and return their input unmodified.

- `GitCommit`:
  - `GitCommit` object (uncompressed, without headers) begins with a series of key-value pairs, with space as the key/value separator, and ends with the commit message, that may span over multiple lines.
  - Values may continue over multiple lines, subsequent lines start with a space which the parser must drop.
  - `GitCommit` fields:
    - `tree` is a reference to a tree object. 
    - `parent` is a reference to the parent of this commit.
    - `author` and `committer` are separate, because the author of a commit is not necessarily the person who can commit it
    - `gpgsig` is the PGP signature of this object.

