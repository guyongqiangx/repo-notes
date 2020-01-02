# repo init

## 附录

### repo init 命令帮助

```text
$ repo help init

Summary
-------
Initialize repo in the current directory

Usage: repo init [options]

Options:
  -h, --help            show this help message and exit

  Logging options:
    -q, --quiet         be quiet

  Manifest options:
    -u URL, --manifest-url=URL
                        manifest repository location
    -b REVISION, --manifest-branch=REVISION
                        manifest branch or revision
    -m NAME.xml, --manifest-name=NAME.xml
                        initial manifest file
    --mirror            create a replica of the remote repositories rather
                        than a client working directory
    --reference=DIR     location of mirror directory
    --depth=DEPTH       create a shallow clone with given depth; see git clone
    --archive           checkout an archive instead of a git repository for
                        each project. See git archive.
    -g GROUP, --groups=GROUP
                        restrict manifest projects to ones with specified
                        group(s) [default|all|G1,G2,G3|G4,-G5,-G6]
    -p PLATFORM, --platform=PLATFORM
                        restrict manifest projects to ones with a specified
                        platform group [auto|all|none|linux|darwin|...]
    --no-clone-bundle   disable use of /clone.bundle on HTTP/HTTPS

  repo Version options:
    --repo-url=URL      repo repository location
    --repo-branch=REVISION
                        repo branch or revision
    --no-repo-verify    do not verify repo source code

  Other options:
    --config-name       Always prompt for name/e-mail

Description
-----------
The 'repo init' command is run once to install and initialize repo. The
latest repo source code and manifest collection is downloaded from the
server and is installed in the .repo/ directory in the current working
directory.

The optional -b argument can be used to select the manifest branch to
checkout and use. If no branch is specified, master is assumed.

The optional -m argument can be used to specify an alternate manifest to
be used. If no manifest is specified, the manifest default.xml will be
used.

The --reference option can be used to point to a directory that has the
content of a --mirror sync. This will make the working directory use as
much data as possible from the local reference directory when fetching
from the server. This will make the sync go a lot faster by reducing
data traffic on the network.

The --no-clone-bundle option disables any attempt to use
$URL/clone.bundle to bootstrap a new Git repository from a resumeable
bundle file on a content delivery network. This may be necessary if
there are problems with the local Python HTTP client or proxy
configuration, but the Git binary works.

Switching Manifest Branches
---------------------------
To switch to another manifest branch, `repo init -b otherbranch` may be
used in an existing client. However, as this only updates the manifest,
a subsequent `repo sync` (or `repo sync -d`) is necessary to update the
working directory files.

$
```

### 最后更新: 2020/01/02

