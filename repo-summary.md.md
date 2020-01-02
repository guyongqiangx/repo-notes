# repo命令帮助信息汇总

有时想查看repo命令的帮助信息，但是每次都需要去某个repo仓库下运行"repo help cmd"命令很不方便，所以这里将其统一汇总到一起。repo命令比较多，以前每个命令都单独运行然后抓取输出，这次写了个脚本，自动运行并保存输出。

本文主要分文两个部分，第1部分汇总repo命令的帮助信息；第2部分附上批量运行repo命令并抓取输出的脚本，输出格式有两种，包括纯文本方式和markdown方式，稍微修改就可以用于其他命令的批量运行，如git命令或bash命令什么的。

> 本文的repo命令帮助汇总信息就是通过markdown方式生成的。

## 1. repo 命令帮助信息汇总

### 索引

* [1. repo abandon]()
* [2. repo branch]()
* [3. repo branches]()
* [4. repo checkout]()
* [5. repo cherry-pick]()
* [6. repo diff]()
* [7. repo diffmanifests]()
* [8. repo download]()
* [9. repo forall]()
* [10. repo gitc-delete]()
* [11. repo gitc-init]()
* [12. repo grep]()
* [13. repo help]()
* [14. repo info]()
* [15. repo init]()
* [16. repo list]()
* [17. repo manifest]()
* [18. repo overview]()
* [19. repo prune]()
* [20. repo rebase]()
* [21. repo selfupdate]()
* [22. repo smartsync]()
* [23. repo stage]()
* [24. repo start]()
* [25. repo status]()
* [26. repo sync]()
* [27. repo upload]()
* [28. repo version]()

### [1. repo abandon]()

```text
$ repo help abandon

Summary
-------
Permanently abandon a development branch

Usage: repo abandon <branchname> [<project>...]

This subcommand permanently abandons a development branch by
deleting it (and all its history) from your local repository.

It is equivalent to "git branch -D <branchname>".

Options:
  -h, --help  show this help message and exit
```

### [2. repo branch]()

```text
$ repo help branch

Summary
-------
View current topic branches

Usage: repo branches [<project>...]

Summarizes the currently available topic branches.

Branch Display
--------------

The branch display output by this command is organized into four
columns of information; for example:

 *P nocolor                   | in repo
    repo2                     |

The first column contains a * if the branch is the currently
checked out branch in any of the specified projects, or a blank
if no project has the branch checked out.

The second column contains either blank, p or P, depending upon
the upload status of the branch.

 (blank): branch not yet published by repo upload
       P: all commits were published by repo upload
       p: only some commits were published by repo upload

The third column contains the branch name.

The fourth column (after the | separator) lists the projects that
the branch appears in, or does not appear in.  If no project list
is shown, then the branch appears in all projects.

Options:
  -h, --help  show this help message and exit
```

### [3. repo branches]()

```text
$ repo help branches

Summary
-------
View current topic branches

Usage: repo branches [<project>...]

Summarizes the currently available topic branches.

Branch Display
--------------

The branch display output by this command is organized into four
columns of information; for example:

 *P nocolor                   | in repo
    repo2                     |

The first column contains a * if the branch is the currently
checked out branch in any of the specified projects, or a blank
if no project has the branch checked out.

The second column contains either blank, p or P, depending upon
the upload status of the branch.

 (blank): branch not yet published by repo upload
       P: all commits were published by repo upload
       p: only some commits were published by repo upload

The third column contains the branch name.

The fourth column (after the | separator) lists the projects that
the branch appears in, or does not appear in.  If no project list
is shown, then the branch appears in all projects.

Options:
  -h, --help  show this help message and exit
```

### [4. repo checkout]()

```text
$ repo help checkout

Summary
-------
Checkout a branch for development

Usage: repo checkout <branchname> [<project>...]

Options:
  -h, --help  show this help message and exit

Description
-----------
The 'repo checkout' command checks out an existing branch that was
previously created by 'repo start'.

The command is equivalent to:

  repo forall [<project>...] -c git checkout <branchname>
```

### [5. repo cherry-pick]()

```text
$ repo help cherry-pick

Summary
-------
Cherry-pick a change.

Usage: repo cherry-pick <sha1>

Options:
  -h, --help  show this help message and exit

Description
-----------
'repo cherry-pick' cherry-picks a change from one branch to another. The
change id will be updated, and a reference to the old change id will be
added.
```

### [6. repo diff]()

```text
$ repo help diff

Summary
-------
Show changes between commit and working tree

Usage: repo diff [<project>...]

The -u option causes 'repo diff' to generate diff output with file paths
relative to the repository root, so the output can be applied
to the Unix 'patch' command.

Options:
  -h, --help      show this help message and exit
  -u, --absolute  Paths are relative to the repository root
```

### [7. repo diffmanifests]()

```text
$ repo help diffmanifests

Summary
-------
Manifest diff utility

Usage: repo diffmanifests manifest1.xml [manifest2.xml] [options]

Options:
  -h, --help            show this help message and exit
  --raw                 Display raw diff.
  --no-color            does not display the diff in color.
  --pretty-format=<FORMAT>
                        print the log using a custom git pretty format string

Description
-----------
The repo diffmanifests command shows differences between project
revisions of manifest1 and manifest2. if manifest2 is not specified,
current manifest.xml will be used instead. Both absolute and relative
paths may be used for manifests. Relative paths start from project's
".repo/manifests" folder.

The --raw option Displays the diff in a way that facilitates parsing,
the project pattern will be <status> <path> <revision from> [<revision
to>] and the commit pattern will be <status> <onelined log> with status
values respectively :

  A = Added project
  R = Removed project
  C = Changed project
  U = Project with unreachable revision(s) (revision(s) not found)

for project, and

   A = Added commit
   R = Removed commit

for a commit.

Only changed projects may contain commits, and commit status always
starts with a space, and are part of last printed project. Unreachable
revisions may occur if project is not up to date or if repo has not been
initialized with all the groups, in which case some projects won't be
synced and their revisions won't be found.
```

### [8. repo download]()

```text
$ repo help download

Summary
-------
Download and checkout a change

Usage: repo download {project change[/patchset]}...

Options:
  -h, --help         show this help message and exit
  -c, --cherry-pick  cherry-pick instead of checkout
  -r, --revert       revert instead of checkout
  -f, --ff-only      force fast-forward merge

Description
-----------
The 'repo download' command downloads a change from the review system
and makes it available in your project's local working directory.
```

### [9. repo forall]()

```text
$ repo help forall

Summary
-------
Run a shell command in each project

Usage: repo forall [<project>...] -c <command> [<arg>...]
repo forall -r str1 [str2] ... -c <command> [<arg>...]"

Options:
  -h, --help            show this help message and exit
  -r, --regex           Execute the command only on projects matching regex or
                        wildcard expression
  -i, --inverse-regex   Execute the command only on projects not matching
                        regex or wildcard expression
  -g GROUPS, --groups=GROUPS
                        Execute the command only on projects matching the
                        specified groups
  -c, --command         Command (and arguments) to execute
  -e, --abort-on-errors
                        Abort if a command exits unsuccessfully

  Output:
    -p                  Show project headers before output
    -v, --verbose       Show command error messages
    -j JOBS, --jobs=JOBS
                        number of commands to execute simultaneously

Description
-----------
Executes the same shell command in each project.

The -r option allows running the command only on projects matching regex
or wildcard expression.

Output Formatting
-----------------
The -p option causes 'repo forall' to bind pipes to the command's stdin,
stdout and stderr streams, and pipe all output into a continuous stream
that is displayed in a single pager session. Project headings are
inserted before the output of each command is displayed. If the command
produces no output in a project, no heading is displayed.

The formatting convention used by -p is very suitable for some types of
searching, e.g. `repo forall -p -c git log -SFoo` will print all commits
that add or remove references to Foo.

The -v option causes 'repo forall' to display stderr messages if a
command produces output only on stderr. Normally the -p option causes
command output to be suppressed until the command produces at least one
byte of output on stdout.

Environment
-----------
pwd is the project's working directory. If the current client is a
mirror client, then pwd is the Git repository.

REPO_PROJECT is set to the unique name of the project.

REPO_PATH is the path relative the the root of the client.

REPO_REMOTE is the name of the remote system from the manifest.

REPO_LREV is the name of the revision from the manifest, translated to a
local tracking branch. If you need to pass the manifest revision to a
locally executed git command, use REPO_LREV.

REPO_RREV is the name of the revision from the manifest, exactly as
written in the manifest.

REPO_COUNT is the total number of projects being iterated.

REPO_I is the current (1-based) iteration count. Can be used in
conjunction with REPO_COUNT to add a simple progress indicator to your
command.

REPO__* are any extra environment variables, specified by the
"annotation" element under any project element. This can be useful for
differentiating trees based on user-specific criteria, or simply
annotating tree details.

shell positional arguments ($1, $2, .., $#) are set to any arguments
following <command>.

Unless -p is used, stdin, stdout, stderr are inherited from the terminal
and are not redirected.

If -e is used, when a command exits unsuccessfully, 'repo forall' will
abort without iterating through the remaining projects.
```

### [10. repo gitc-delete]()

```text
$ repo help gitc-delete

Summary
-------
Delete a GITC Client.

Usage: repo gitc-delete

Options:
  -h, --help   show this help message and exit
  -f, --force  Force the deletion (no prompt).

Description
-----------
This subcommand deletes the current GITC client, deleting the GITC
manifest and all locally downloaded sources.
```

### [11. repo gitc-init]()

```text
$ repo help gitc-init

Summary
-------
Initialize a GITC Client.

Usage: repo gitc-init [options] [client name]

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

  GITC options:
    -f MANIFEST_FILE, --manifest-file=MANIFEST_FILE
                        Optional manifest file to use for this GITC client.
    -c GITC_CLIENT, --gitc-client=GITC_CLIENT
                        The name of the gitc_client instance to create or
                        modify.

Description
-----------
The 'repo gitc-init' command is ran to initialize a new GITC client for
use with the GITC file system.

This command will setup the client directory, initialize repo, just like
repo init does, and then downloads the manifest collection and installs
it in the .repo/directory of the GITC client.

Once this is done, a GITC manifest is generated by pulling the HEAD SHA
for each project and generates the properly formatted XML file and
installs it as .manifest in the GITC client directory.

The -c argument is required to specify the GITC client name.

The optional -f argument can be used to specify the manifest file to use
for this GITC client.
```

### [12. repo grep]()

```text
$ repo help grep

Summary
-------
Print lines matching a pattern

Usage: repo grep {pattern | -e pattern} [<project>...]

Options:
  -h, --help            show this help message and exit

  Sources:
    --cached            Search the index, instead of the work tree
    -r TREEish, --revision=TREEish
                        Search TREEish, instead of the work tree

  Pattern:
    -e PATTERN          Pattern to search for
    -i, --ignore-case   Ignore case differences
    -a, --text          Process binary files as if they were text
    -I                  Don't match the pattern in binary files
    -w, --word-regexp   Match the pattern only at word boundaries
    -v, --invert-match  Select non-matching lines
    -G, --basic-regexp  Use POSIX basic regexp for patterns (default)
    -E, --extended-regexp
                        Use POSIX extended regexp for patterns
    -F, --fixed-strings
                        Use fixed strings (not regexp) for pattern

  Pattern Grouping:
    --all-match         Limit match to lines that have all patterns
    --and, --or, --not  Boolean operators to combine patterns
    -(, -)              Boolean operator grouping

  Output:
    -n                  Prefix the line number to matching lines
    -C CONTEXT          Show CONTEXT lines around match
    -B CONTEXT          Show CONTEXT lines before match
    -A CONTEXT          Show CONTEXT lines after match
    -l, --name-only, --files-with-matches
                        Show only file names containing matching lines
    -L, --files-without-match
                        Show only file names not containing matching lines

Description
-----------
Search for the specified patterns in all project files.

Boolean Options
---------------
The following options can appear as often as necessary to express the
pattern to locate:

 -e PATTERN
 --and, --or, --not, -(, -)

Further, the -r/--revision option may be specified multiple times in
order to scan multiple trees. If the same file matches in more than one
tree, only the first result is reported, prefixed by the revision name
it was found under.

Examples
--------
Look for a line that has '#define' and either 'MAX_PATH or 'PATH_MAX':

  repo grep -e '#define' --and -\( -e MAX_PATH -e PATH_MAX \)

Look for a line that has 'NODE' or 'Unexpected' in files that contain a
line that matches both expressions:

  repo grep --all-match -e NODE -e Unexpected
```

### [13. repo help]()

```text
$ repo help help

Summary
-------
Display detailed help on a command

Usage: repo help [--all|command]

Options:
  -h, --help  show this help message and exit
  -a, --all   show the complete list of commands

Description
-----------
Displays detailed usage information about a command.
```

### [14. repo info]()

```text
$ repo help info

Summary
-------
Get info on the manifest branch, current branch or unmerged branches

Usage: repo info [-dl] [-o [-b]] [<project>...]

Options:
  -h, --help            show this help message and exit
  -d, --diff            show full info and commit diff including remote
                        branches
  -o, --overview        show overview of all local commits
  -b, --current-branch  consider only checked out branches
  -l, --local-only      Disable all remote operations
```

### [15. repo init]()

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
```

### [16. repo list]()

```text
$ repo help list

Summary
-------
List projects and their associated directories

Usage: repo list [-f] [<project>...]
repo list [-f] -r str1 [str2]..."

Options:
  -h, --help            show this help message and exit
  -r, --regex           Filter the project list based on regex or wildcard
                        matching of strings
  -g GROUPS, --groups=GROUPS
                        Filter the project list based on the groups the
                        project is in
  -f, --fullpath        Display the full work tree path instead of the
                        relative path
  -n, --name-only       Display only the name of the repository
  -p, --path-only       Display only the path of the repository

Description
-----------
List all projects; pass '.' to list the project for the cwd.

This is similar to running: repo forall -c 'echo "$REPO_PATH :
$REPO_PROJECT"'.
```

### [17. repo manifest]()

```text
$ repo help manifest

Summary
-------
Manifest inspection utility

Usage: repo manifest [-o {-|NAME.xml} [-r]]

Options:
  -h, --help            show this help message and exit
  -r, --revision-as-HEAD
                        Save revisions as current HEAD
  --suppress-upstream-revision
                        If in -r mode, do not write the upstream field.  Only
                        of use if the branch names for a sha1 manifest are
                        sensitive.
  -o -|NAME.xml, --output-file=-|NAME.xml
                        File to save the manifest to

Description
-----------
With the -o option, exports the current manifest for inspection. The
manifest and (if present) local_manifest.xml are combined together to
produce a single manifest file. This file can be stored in a Git
repository for use during future 'repo init' invocations.

repo Manifest Format
====================
A repo manifest describes the structure of a repo client; that is the
directories that are visible and where they should be obtained from with
git.

The basic structure of a manifest is a bare Git repository holding a
single 'default.xml' XML file in the top level directory.

Manifests are inherently version controlled, since they are kept within
a Git repository. Updates to manifests are automatically obtained by
clients during `repo sync`.

XML File Format
---------------
A manifest XML file (e.g. 'default.xml') roughly conforms to the
following DTD:

  <!DOCTYPE manifest [
    <!ELEMENT manifest (notice?,
                        remote*,
                        default?,
                        manifest-server?,
                        remove-project*,
                        project*,
                        extend-project*,
                        repo-hooks?)>

    <!ELEMENT notice (#PCDATA)>

    <!ELEMENT remote (EMPTY)>
    <!ATTLIST remote name         ID    #REQUIRED>
    <!ATTLIST remote alias        CDATA #IMPLIED>
    <!ATTLIST remote fetch        CDATA #REQUIRED>
    <!ATTLIST remote pushurl      CDATA #IMPLIED>
    <!ATTLIST remote review       CDATA #IMPLIED>
    <!ATTLIST remote revision     CDATA #IMPLIED>

    <!ELEMENT default (EMPTY)>
    <!ATTLIST default remote      IDREF #IMPLIED>
    <!ATTLIST default revision    CDATA #IMPLIED>
    <!ATTLIST default dest-branch CDATA #IMPLIED>
    <!ATTLIST default sync-j      CDATA #IMPLIED>
    <!ATTLIST default sync-c      CDATA #IMPLIED>
    <!ATTLIST default sync-s      CDATA #IMPLIED>

    <!ELEMENT manifest-server (EMPTY)>
    <!ATTLIST manifest-server url CDATA #REQUIRED>

    <!ELEMENT project (annotation*,
                       project*,
                       copyfile*,
                       linkfile*)>
    <!ATTLIST project name        CDATA #REQUIRED>
    <!ATTLIST project path        CDATA #IMPLIED>
    <!ATTLIST project remote      IDREF #IMPLIED>
    <!ATTLIST project revision    CDATA #IMPLIED>
    <!ATTLIST project dest-branch CDATA #IMPLIED>
    <!ATTLIST project groups      CDATA #IMPLIED>
    <!ATTLIST project sync-c      CDATA #IMPLIED>
    <!ATTLIST project sync-s      CDATA #IMPLIED>
    <!ATTLIST project upstream CDATA #IMPLIED>
    <!ATTLIST project clone-depth CDATA #IMPLIED>
    <!ATTLIST project force-path CDATA #IMPLIED>

    <!ELEMENT annotation (EMPTY)>
    <!ATTLIST annotation name  CDATA #REQUIRED>
    <!ATTLIST annotation value CDATA #REQUIRED>
    <!ATTLIST annotation keep  CDATA "true">

    <!ELEMENT copyfile (EMPTY)>
    <!ATTLIST copyfile src  CDATA #REQUIRED>
    <!ATTLIST copyfile dest CDATA #REQUIRED>

    <!ELEMENT linkfile (EMPTY)>
    <!ATTLIST linkfile src CDATA #REQUIRED>
    <!ATTLIST linkfile dest CDATA #REQUIRED>

    <!ELEMENT extend-project (EMPTY)>
    <!ATTLIST extend-project name CDATA #REQUIRED>
    <!ATTLIST extend-project path CDATA #IMPLIED>
    <!ATTLIST extend-project groups CDATA #IMPLIED>

    <!ELEMENT remove-project (EMPTY)>
    <!ATTLIST remove-project name  CDATA #REQUIRED>

    <!ELEMENT repo-hooks (EMPTY)>
    <!ATTLIST repo-hooks in-project CDATA #REQUIRED>
    <!ATTLIST repo-hooks enabled-list CDATA #REQUIRED>

    <!ELEMENT include      (EMPTY)>
    <!ATTLIST include name CDATA #REQUIRED>
  ]>

A description of the elements and their attributes follows.

Element manifest
----------------
The root element of the file.

Element remote
--------------
One or more remote elements may be specified. Each remote element
specifies a Git URL shared by one or more projects and (optionally) the
Gerrit review server those projects upload changes through.

Attribute `name`: A short name unique to this manifest file. The name
specified here is used as the remote name in each project's .git/config,
and is therefore automatically available to commands like `git fetch`,
`git remote`, `git pull` and `git push`.

Attribute `alias`: The alias, if specified, is used to override `name`
to be set as the remote name in each project's .git/config. Its value
can be duplicated while attribute `name` has to be unique in the
manifest file. This helps each project to be able to have same remote
name which actually points to different remote url.

Attribute `fetch`: The Git URL prefix for all projects which use this
remote. Each project's name is appended to this prefix to form the
actual URL used to clone the project.

Attribute `pushurl`: The Git "push" URL prefix for all projects which
use this remote. Each project's name is appended to this prefix to form
the actual URL used to "git push" the project. This attribute is
optional; if not specified then "git push" will use the same URL as the
`fetch` attribute.

Attribute `review`: Hostname of the Gerrit server where reviews are
uploaded to by `repo upload`. This attribute is optional; if not
specified then `repo upload` will not function.

Attribute `revision`: Name of a Git branch (e.g. `master` or
`refs/heads/master`). Remotes with their own revision will override the
default revision.

Element default
---------------
At most one default element may be specified. Its remote and revision
attributes are used when a project element does not specify its own
remote or revision attribute.

Attribute `remote`: Name of a previously defined remote element. Project
elements lacking a remote attribute of their own will use this remote.

Attribute `revision`: Name of a Git branch (e.g. `master` or
`refs/heads/master`). Project elements lacking their own revision
attribute will use this revision.

Attribute `dest-branch`: Name of a Git branch (e.g. `master`). Project
elements not setting their own `dest-branch` will inherit this value. If
this value is not set, projects will use `revision` by default instead.

Attribute `sync-j`: Number of parallel jobs to use when synching.

Attribute `sync-c`: Set to true to only sync the given Git branch
(specified in the `revision` attribute) rather than the whole ref space.
Project elements lacking a sync-c element of their own will use this
value.

Attribute `sync-s`: Set to true to also sync sub-projects.

Element manifest-server
-----------------------
At most one manifest-server may be specified. The url attribute is used
to specify the URL of a manifest server, which is an XML RPC service.

The manifest server should implement the following RPC methods:

  GetApprovedManifest(branch, target)

Return a manifest in which each project is pegged to a known good
revision for the current branch and target. This is used by repo sync
when the --smart-sync option is given.

The target to use is defined by environment variables TARGET_PRODUCT and
TARGET_BUILD_VARIANT. These variables are used to create a string of the
form $TARGET_PRODUCT-$TARGET_BUILD_VARIANT, e.g. passion-userdebug. If
one of those variables or both are not present, the program will call
GetApprovedManifest without the target parameter and the manifest server
should choose a reasonable default target.

  GetManifest(tag)

Return a manifest in which each project is pegged to the revision at the
specified tag. This is used by repo sync when the --smart-tag option is
given.

Element project
---------------
One or more project elements may be specified. Each element describes a
single Git repository to be cloned into the repo client workspace. You
may specify Git-submodules by creating a nested project. Git-submodules
will be automatically recognized and inherit their parent's attributes,
but those may be overridden by an explicitly specified project element.

Attribute `name`: A unique name for this project. The project's name is
appended onto its remote's fetch URL to generate the actual URL to
configure the Git remote with. The URL gets formed as:

  ${remote_fetch}/${project_name}.git

where ${remote_fetch} is the remote's fetch attribute and
${project_name} is the project's name attribute. The suffix ".git" is
always appended as repo assumes the upstream is a forest of bare Git
repositories. If the project has a parent element, its name will be
prefixed by the parent's.

The project name must match the name Gerrit knows, if Gerrit is being
used for code reviews.

Attribute `path`: An optional path relative to the top directory of the
repo client where the Git working directory for this project should be
placed. If not supplied the project name is used. If the project has a
parent element, its path will be prefixed by the parent's.

Attribute `remote`: Name of a previously defined remote element. If not
supplied the remote given by the default element is used.

Attribute `revision`: Name of the Git branch the manifest wants to track
for this project. Names can be relative to refs/heads (e.g. just
"master") or absolute (e.g. "refs/heads/master"). Tags and/or explicit
SHA-1s should work in theory, but have not been extensively tested. If
not supplied the revision given by the remote element is used if
applicable, else the default element is used.

Attribute `dest-branch`: Name of a Git branch (e.g. `master`). When
using `repo upload`, changes will be submitted for code review on this
branch. If unspecified both here and in the default element, `revision`
is used instead.

Attribute `groups`: List of groups to which this project belongs,
whitespace or comma separated. All projects belong to the group "all",
and each project automatically belongs to a group of its name:`name` and
path:`path`. E.g. for <project name="monkeys" path="barrel-of"/>, that
project definition is implicitly in the following manifest groups:
default, name:monkeys, and path:barrel-of. If you place a project in the
group "notdefault", it will not be automatically downloaded by repo. If
the project has a parent element, the `name` and `path` here are the
prefixed ones.

Attribute `sync-c`: Set to true to only sync the given Git branch
(specified in the `revision` attribute) rather than the whole ref space.

Attribute `sync-s`: Set to true to also sync sub-projects.

Attribute `upstream`: Name of the Git ref in which a sha1 can be found.
Used when syncing a revision locked manifest in -c mode to avoid having
to sync the entire ref space.

Attribute `clone-depth`: Set the depth to use when fetching this
project. If specified, this value will override any value given to repo
init with the --depth option on the command line.

Attribute `force-path`: Set to true to force this project to create the
local mirror repository according to its `path` attribute (if supplied)
rather than the `name` attribute. This attribute only applies to the
local mirrors syncing, it will be ignored when syncing the projects in a
client working directory.

Element extend-project
----------------------
Modify the attributes of the named project.

This element is mostly useful in a local manifest file, to modify the
attributes of an existing project without completely replacing the
existing project definition. This makes the local manifest more robust
against changes to the original manifest.

Attribute `path`: If specified, limit the change to projects checked out
at the specified path, rather than all projects with the given name.

Attribute `groups`: List of additional groups to which this project
belongs. Same syntax as the corresponding element of `project`.

Element annotation
------------------
Zero or more annotation elements may be specified as children of a
project element. Each element describes a name-value pair that will be
exported into each project's environment during a 'forall' command,
prefixed with REPO__. In addition, there is an optional attribute "keep"
which accepts the case insensitive values "true" (default) or "false".
This attribute determines whether or not the annotation will be kept
when exported with the manifest subcommand.

Element copyfile
----------------
Zero or more copyfile elements may be specified as children of a project
element. Each element describes a src-dest pair of files; the "src" file
will be copied to the "dest" place during 'repo sync' command. "src" is
project relative, "dest" is relative to the top of the tree.

Element linkfile
----------------
It's just like copyfile and runs at the same time as copyfile but
instead of copying it creates a symlink.

Element remove-project
----------------------
Deletes the named project from the internal manifest table, possibly
allowing a subsequent project element in the same manifest file to
replace the project with a different source.

This element is mostly useful in a local manifest file, where the user
can remove a project, and possibly replace it with their own definition.

Element include
---------------
This element provides the capability of including another manifest file
into the originating manifest. Normal rules apply for the target
manifest to include - it must be a usable manifest on its own.

Attribute `name`: the manifest to include, specified relative to the
manifest repository's root.

Local Manifests
===============
Additional remotes and projects may be added through local manifest
files stored in `$TOP_DIR/.repo/local_manifests/*.xml`.

For example:

  $ ls .repo/local_manifests
  local_manifest.xml
  another_local_manifest.xml

  $ cat .repo/local_manifests/local_manifest.xml
  <?xml version="1.0" encoding="UTF-8"?>
  <manifest>
    <project path="manifest"
             name="tools/manifest" />
    <project path="platform-manifest"
             name="platform/manifest" />
  </manifest>

Users may add projects to the local manifest(s) prior to a `repo sync`
invocation, instructing repo to automatically download and manage these
extra projects.

Manifest files stored in `$TOP_DIR/.repo/local_manifests/*.xml` will be
loaded in alphabetical order.

Additional remotes and projects may also be added through a local
manifest, stored in `$TOP_DIR/.repo/local_manifest.xml`. This method is
deprecated in favor of using multiple manifest files as mentioned above.

If `$TOP_DIR/.repo/local_manifest.xml` exists, it will be loaded before
any manifest files stored in `$TOP_DIR/.repo/local_manifests/*.xml`.
```

### [18. repo overview]()

```text
$ repo help overview

Summary
-------
Display overview of unmerged project branches

Usage: repo overview [--current-branch] [<project>...]

Options:
  -h, --help            show this help message and exit
  -b, --current-branch  Consider only checked out branches

Description
-----------
The 'repo overview' command is used to display an overview of the
projects branches, and list any local commits that have not yet been
merged into the project.

The -b/--current-branch option can be used to restrict the output to
only branches currently checked out in each project. By default, all
branches are displayed.
```

### [19. repo prune]()

```text
$ repo help prune

Summary
-------
Prune (delete) already merged topics

Usage: repo prune [<project>...]

Options:
  -h, --help  show this help message and exit
```

### [20. repo rebase]()

```text
$ repo help rebase

Summary
-------
Rebase local branches on upstream branch

Usage: repo rebase {[<project>...] | -i <project>...}

Options:
  -h, --help           show this help message and exit
  -i, --interactive    interactive rebase (single project only)
  -f, --force-rebase   Pass --force-rebase to git rebase
  --no-ff              Pass --no-ff to git rebase
  -q, --quiet          Pass --quiet to git rebase
  --autosquash         Pass --autosquash to git rebase
  --whitespace=WS      Pass --whitespace to git rebase
  --auto-stash         Stash local modifications before starting
  -m, --onto-manifest  Rebase onto the manifest version instead of upstream
                       HEAD.  This helps to make sure the local tree stays
                       consistent if you previously synced to a manifest.

Description
-----------
'repo rebase' uses git rebase to move local changes in the current topic
branch to the HEAD of the upstream history, useful when you have made
commits in a topic branch but need to incorporate new upstream changes
"underneath" them.
```

### [21. repo selfupdate]()

```text
$ repo help selfupdate

Summary
-------
Update repo to the latest version

Usage: repo selfupdate

Options:
  -h, --help          show this help message and exit

  repo Version options:
    --no-repo-verify  do not verify repo source code

Description
-----------
The 'repo selfupdate' command upgrades repo to the latest version, if a
newer version is available.

Normally this is done automatically by 'repo sync' and does not need to
be performed by an end-user.
```

### [22. repo smartsync]()

```text
$ repo help smartsync

Summary
-------
Update working tree to the latest known good revision

Usage: repo smartsync [<project>...]

Options:
  -h, --help            show this help message and exit
  -f, --force-broken    continue sync even if a project fails to sync
  --force-sync          overwrite an existing git directory if it needs to
                        point to a different object directory. WARNING: this
                        may cause loss of data
  -l, --local-only      only update working tree, don't fetch
  -n, --network-only    fetch only, don't update working tree
  -d, --detach          detach projects back to manifest revision
  -c, --current-branch  fetch only current branch from server
  -q, --quiet           be more quiet
  -j JOBS, --jobs=JOBS  projects to fetch simultaneously (default 1)
  -m NAME.xml, --manifest-name=NAME.xml
                        temporary manifest to use for this sync
  --no-clone-bundle     disable use of /clone.bundle on HTTP/HTTPS
  -u MANIFEST_SERVER_USERNAME, --manifest-server-username=MANIFEST_SERVER_USERNAME
                        username to authenticate with the manifest server
  -p MANIFEST_SERVER_PASSWORD, --manifest-server-password=MANIFEST_SERVER_PASSWORD
                        password to authenticate with the manifest server
  --fetch-submodules    fetch submodules from server
  --no-tags             don't fetch tags
  --optimized-fetch     only fetch projects fixed to sha1 if revision does not
                        exist locally
  --prune               delete refs that no longer exist on the remote

  repo Version options:
    --no-repo-verify    do not verify repo source code

Description
-----------
The 'repo smartsync' command is a shortcut for sync -s.
```

### [23. repo stage]()

```text
$ repo help stage

Summary
-------
Stage file(s) for commit

Usage: repo stage -i [<project>...]

Options:
  -h, --help         show this help message and exit
  -i, --interactive  use interactive staging

Description
-----------
The 'repo stage' command stages files to prepare the next commit.
```

### [24. repo start]()

```text
$ repo help start

Summary
-------
Start a new branch for development

Usage: repo start <newbranchname> [--all | <project>...]

Options:
  -h, --help  show this help message and exit
  --all       begin branch in all projects

Description
-----------
'repo start' begins a new branch of development, starting from the
revision specified in the manifest.
```

### [25. repo status]()

```text
$ repo help status

Summary
-------
Show the working tree status

Usage: repo status [<project>...]

Options:
  -h, --help            show this help message and exit
  -j JOBS, --jobs=JOBS  number of projects to check simultaneously
  -o, --orphans         include objects in working directory outside of repo
                        projects

Description
-----------
'repo status' compares the working tree to the staging area (aka index),
and the most recent commit on this branch (HEAD), in each project
specified. A summary is displayed, one line per file where there is a
difference between these three states.

The -j/--jobs option can be used to run multiple status queries in
parallel.

The -o/--orphans option can be used to show objects that are in the
working directory, but not associated with a repo project. This includes
unmanaged top-level files and directories, but also includes deeper
items. For example, if dir/subdir/proj1 and dir/subdir/proj2 are repo
projects, dir/subdir/proj3 will be shown if it is not known to repo.

Status Display
--------------
The status display is organized into three columns of information, for
example if the file 'subcmds/status.py' is modified in the project
'repo' on branch 'devwork':

  project repo/                                   branch devwork
   -m     subcmds/status.py

The first column explains how the staging area (index) differs from the
last commit (HEAD). Its values are always displayed in upper case and
have the following meanings:

 -:  no difference
 A:  added         (not in HEAD,     in index                     )
 M:  modified      (    in HEAD,     in index, different content  )
 D:  deleted       (    in HEAD, not in index                     )
 R:  renamed       (not in HEAD,     in index, path changed       )
 C:  copied        (not in HEAD,     in index, copied from another)
 T:  mode changed  (    in HEAD,     in index, same content       )
 U:  unmerged; conflict resolution required

The second column explains how the working directory differs from the
index. Its values are always displayed in lower case and have the
following meanings:

 -:  new / unknown (not in index,     in work tree                )
 m:  modified      (    in index,     in work tree, modified      )
 d:  deleted       (    in index, not in work tree                )
```

### [26. repo sync]()

```text
$ repo help sync

Summary
-------
Update working tree to the latest revision

Usage: repo sync [<project>...]

Options:
  -h, --help            show this help message and exit
  -f, --force-broken    continue sync even if a project fails to sync
  --force-sync          overwrite an existing git directory if it needs to
                        point to a different object directory. WARNING: this
                        may cause loss of data
  -l, --local-only      only update working tree, don't fetch
  -n, --network-only    fetch only, don't update working tree
  -d, --detach          detach projects back to manifest revision
  -c, --current-branch  fetch only current branch from server
  -q, --quiet           be more quiet
  -j JOBS, --jobs=JOBS  projects to fetch simultaneously (default 1)
  -m NAME.xml, --manifest-name=NAME.xml
                        temporary manifest to use for this sync
  --no-clone-bundle     disable use of /clone.bundle on HTTP/HTTPS
  -u MANIFEST_SERVER_USERNAME, --manifest-server-username=MANIFEST_SERVER_USERNAME
                        username to authenticate with the manifest server
  -p MANIFEST_SERVER_PASSWORD, --manifest-server-password=MANIFEST_SERVER_PASSWORD
                        password to authenticate with the manifest server
  --fetch-submodules    fetch submodules from server
  --no-tags             don't fetch tags
  --optimized-fetch     only fetch projects fixed to sha1 if revision does not
                        exist locally
  --prune               delete refs that no longer exist on the remote
  -s, --smart-sync      smart sync using manifest from the latest known good
                        build
  -t SMART_TAG, --smart-tag=SMART_TAG
                        smart sync using manifest from a known tag

  repo Version options:
    --no-repo-verify    do not verify repo source code

Description
-----------
The 'repo sync' command synchronizes local project directories with the
remote repositories specified in the manifest. If a local project does
not yet exist, it will clone a new local directory from the remote
repository and set up tracking branches as specified in the manifest. If
the local project already exists, 'repo sync' will update the remote
branches and rebase any new local changes on top of the new remote
changes.

'repo sync' will synchronize all projects listed at the command line.
Projects can be specified either by name, or by a relative or absolute
path to the project's local directory. If no projects are specified,
'repo sync' will synchronize all projects listed in the manifest.

The -d/--detach option can be used to switch specified projects back to
the manifest revision. This option is especially helpful if the project
is currently on a topic branch, but the manifest revision is temporarily
needed.

The -s/--smart-sync option can be used to sync to a known good build as
specified by the manifest-server element in the current manifest. The
-t/--smart-tag option is similar and allows you to specify a custom
tag/label.

The -u/--manifest-server-username and -p/--manifest-server-password
options can be used to specify a username and password to authenticate
with the manifest server when using the -s or -t option.

If -u and -p are not specified when using the -s or -t option, 'repo
sync' will attempt to read authentication credentials for the manifest
server from the user's .netrc file.

'repo sync' will not use authentication credentials from -u/-p or .netrc
if the manifest server specified in the manifest file already includes
credentials.

The -f/--force-broken option can be used to proceed with syncing other
projects if a project sync fails.

The --force-sync option can be used to overwrite existing git
directories if they have previously been linked to a different object
direcotry. WARNING: This may cause data to be lost since refs may be
removed when overwriting.

The --no-clone-bundle option disables any attempt to use
$URL/clone.bundle to bootstrap a new Git repository from a resumeable
bundle file on a content delivery network. This may be necessary if
there are problems with the local Python HTTP client or proxy
configuration, but the Git binary works.

The --fetch-submodules option enables fetching Git submodules of a
project from server.

The -c/--current-branch option can be used to only fetch objects that
are on the branch specified by a project's revision.

The --optimized-fetch option can be used to only fetch projects that are
fixed to a sha1 revision if the sha1 revision does not already exist
locally.

The --prune option can be used to remove any refs that no longer exist
on the remote.

SSH Connections
---------------
If at least one project remote URL uses an SSH connection (ssh://,
git+ssh://, or user@host:path syntax) repo will automatically enable the
SSH ControlMaster option when connecting to that host. This feature
permits other projects in the same 'repo sync' session to reuse the same
SSH tunnel, saving connection setup overheads.

To disable this behavior on UNIX platforms, set the GIT_SSH environment
variable to 'ssh'. For example:

  export GIT_SSH=ssh
  repo sync

  Compatibility
  ~~~~~~~~~~~~~
This feature is automatically disabled on Windows, due to the lack of
UNIX domain socket support.

This feature is not compatible with url.insteadof rewrites in the user's
~/.gitconfig. 'repo sync' is currently not able to perform the rewrite
early enough to establish the ControlMaster tunnel.

If the remote SSH daemon is Gerrit Code Review, version 2.0.10 or later
is required to fix a server side protocol bug.
```

### [27. repo upload]()

```text
$ repo help upload

Summary
-------
Upload changes for code review

Usage: repo upload [--re --cc] [<project>]...

Options:
  -h, --help            show this help message and exit
  -t                    Send local branch name to Gerrit Code Review
  --re=REVIEWERS, --reviewers=REVIEWERS
                        Request reviews from these people.
  --cc=CC               Also send email to these email addresses.
  --br=BRANCH           Branch to upload.
  --cbr, --current-branch
                        Upload current git branch.
  -d, --draft           If specified, upload as a draft.
  -D BRANCH, --destination=BRANCH, --dest=BRANCH
                        Submit for review on this target branch.
  --no-verify           Do not run the upload hook.
  --verify              Run the upload hook without prompting.

Description
-----------
The 'repo upload' command is used to send changes to the Gerrit Code
Review system. It searches for topic branches in local projects that
have not yet been published for review. If multiple topic branches are
found, 'repo upload' opens an editor to allow the user to select which
branches to upload.

'repo upload' searches for uploadable changes in all projects listed at
the command line. Projects can be specified either by name, or by a
relative or absolute path to the project's local directory. If no
projects are specified, 'repo upload' will search for uploadable changes
in all projects listed in the manifest.

If the --reviewers or --cc options are passed, those emails are added to
the respective list of users, and emails are sent to any new users.
Users passed as --reviewers must already be registered with the code
review system, or the upload will fail.

Configuration
-------------
review.URL.autoupload:

To disable the "Upload ... (y/N)?" prompt, you can set a per-project or
global Git configuration option. If review.URL.autoupload is set to
"true" then repo will assume you always answer "y" at the prompt, and
will not prompt you further. If it is set to "false" then repo will
assume you always answer "n", and will abort.

review.URL.autoreviewer:

To automatically append a user or mailing list to reviews, you can set a
per-project or global Git option to do so.

review.URL.autocopy:

To automatically copy a user or mailing list to all uploaded reviews,
you can set a per-project or global Git option to do so. Specifically,
review.URL.autocopy can be set to a comma separated list of reviewers
who you always want copied on all uploads with a non-empty --re
argument.

review.URL.username:

Override the username used to connect to Gerrit Code Review. By default
the local part of the email address is used.

The URL must match the review URL listed in the manifest XML file, or in
the .git/config within the project. For example:

  [remote "origin"]
    url = git://git.example.com/project.git
    review = http://review.example.com/

  [review "http://review.example.com/"]
    autoupload = true
    autocopy = johndoe@company.com,my-team-alias@company.com

review.URL.uploadtopic:

To add a topic branch whenever uploading a commit, you can set a
per-project or global Git option to do so. If review.URL.uploadtopic is
set to "true" then repo will assume you always want the equivalent of
the -t option to the repo command. If unset or set to "false" then repo
will make use of only the command line option.

References
----------
Gerrit Code Review: http://code.google.com/p/gerrit/
```

### [28. repo version]()

```text
$ repo help version

Summary
-------
Display the version of repo

Usage: repo version

Options:
  -h, --help  show this help message and exit
```

## 2. 批量运行repo命令并抓取输出的脚本

### 2.1 纯文本格式

抓取所有的帮助信息并存放到文本文件中。

在某个repo仓库的根目录下执行`repo help cmd`，并将所有命令输出到指定文件中，内容如下：

```text
#!/bin/bash

out_file=$1

$(rm -rf $out_file)

cmds=$(repo help --all | grep -E "^ " | cut -d' ' -f3)

for cmd in $cmds
do
    echo
    echo "\$ repo help $cmd"
    # echo # There's a new line here
    echo "$(repo help $cmd)"
    echo
    echo "************************************************************************"
done | tee -a $out_file

echo done!
```

执行的命令如下：

```text
op-tee/arm-v8$ ./repo-cmd-msg.sh repo-help.txt
op-tee/arm-v8$ head -20 repo-help.txt

$ repo help abandon

Summary
-------
Permanently abandon a development branch

Usage: repo abandon <branchname> [<project>...]

This subcommand permanently abandons a development branch by
deleting it (and all its history) from your local repository.

It is equivalent to "git branch -D <branchname>".

Options:
  -h, --help  show this help message and exit

************************************************************************
```

### 2.2 Markdown格式

Markdown格式添加了索引，点击索引命令到达命令帮助的详细信息，点击帮助信息的标题回到索引处。

```text
#!/bin/bash

out_file=$1

$(rm -rf $out_file)

# 使用 "_write xxx" 代替 "echo xxx | tee -a $out_file"
function _write()
{
    echo "$1" | tee -a $out_file
}

cmds=$(repo help --all | grep -E "^ " | cut -d' ' -f3)

# 生成头部索引
_write "<span id=\"__TOP\">索引</span>"
i=1
for cmd in $cmds
do
    _write "- [$i. repo $cmd](#__$cmd)"
    i=$((i+1))
done

_write "---"

# 生成详细内容
i=1
for cmd in $cmds
do
    _write "## <span id=\"__$cmd\">[$i. repo $cmd](#__TOP)</span>"
    _write "\`\`\`"
    _write "\$ repo help $cmd"
    # _write ""
    _write "$(repo help $cmd)"
    _write "\`\`\`"
    _write ""

    i=$((i+1))
done

echo done!
```

## 3. 联系和福利

洛奇工作中常常会遇到自己不熟悉的问题，这些问题可能并不难，但因为不了解，找不到人帮忙而瞎折腾，往往导致浪费几天甚至更久的时间。

所以我组建了两个微信讨论群\(记得微信我说加哪个群，如何加微信见后面\)，欢迎加群一起讨论:

* 一个Android OTA的讨论组，请说明加Android OTA群。
* 一个git和repo的讨论组，请说明加git和repo群。

在工作之余，洛奇尽量写一些对大家有用的东西，如果洛奇的这篇文章让您有所收获，解决了您一直以来未能解决的问题，不妨赞赏一下洛奇，这也是对洛奇付出的最大鼓励。扫下面的二维码赞赏洛奇，金额随意：

![&#x6536;&#x94B1;&#x7801;](https://img-blog.csdnimg.cn/20190111150810383.png)

洛奇自己维护了一个公众号“洛奇看世界”，一个关注程序员转型，提升认知的公众号，不定期更新。公号也提供个人联系方式，一些Andorid和GIT电子书资源，说不定会有意外的收获，详细内容见公号提示。扫下面的二维码关注公众号：

![&#x516C;&#x4F17;&#x53F7;](https://img-blog.csdnimg.cn/20190111150824695.png)

如果您觉得我想钱想疯了，或者套路公众号加粉，那请忽略以上文字，看看就好。我相信，如果您自己有做分享，有做公众号，那您会理解我的。

谢谢！

