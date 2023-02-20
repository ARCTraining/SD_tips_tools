# Git glossary

```{glossary}
changeset
    A group of changes to one or more files that are or will be added
    to a single {term}`commit` in a {term}`version control`
    {term}`repository`.

commit
    To record the current state of a set of files (a {term}`changeset`)
    in a {term}`version control` {term}`repository`. As a noun,
    the result of committing, i.e. a recorded changeset in a repository.
    If a commit contains changes to multiple files,
    all of the changes are recorded together.

conflict
    A change made by one user of a {term}`version control` system
    that is incompatible with changes made by other users.
    Helping users {term}`resolve` conflicts
    is one of version control's major tasks.

HTTP
    The Hypertext Transfer {term}`Protocol` used for sharing web pages and other data
    on the World Wide Web.

merge
    (a repository): To reconcile two sets of changes to a
    {term}`repository`.

protocol
    A set of rules that define how one computer communicates with another.
    Common protocols on the Internet include {term}`HTTP` and {term}`SSH`.

remote
    (of a repository) A version control {term}`repository` connected to another,
    in such way that both can be kept in sync exchanging {term}`commit`s.

repository
    A storage area where a {term}`version control` system
    stores the full history of {term}`commit`s of a project and information
    about who changed what, when.

resolve
    To eliminate the {term}`conflict`s between two or more incompatible changes to a file or set of files
    being managed by a {term}`version control` system.

revision
    A synonym for {term}`commit`.

SHA-1
    {term}`SHA-1` hashes is what Git uses to compute identifiers, including for commits.
    To compute these, Git uses not only the actual change of a commit, but also its metadata (such as date, author,
    message), including the identifiers of all commits of preceding changes. This makes Git commit IDs virtually unique.
    I.e., the likelihood that two commits made independently, even of the same change, receive the same ID is exceedingly
    small.

SSH
    The Secure Shell {term}`protocol` used for secure communication between computers.

timestamp
    A record of when a particular event occurred.

version control
    A tool for managing changes to a set of files.
    Each set of changes creates a new {term}`commit` of the files;
    the version control system allows users to recover old commits reliably,
    and helps manage conflicting changes made by different users.

```

## Git cheatsheets for quick reference

* A great [printable git cheatsheet](https://education.github.com/git-cheat-sheet-education.pdf) is available in PDF from the
[GitHub Education website](https://education.github.com/).
* An [interactive one-page visualisation](http://ndpsoftware.com/git-cheatsheet.html)
    about the relationships between workspace, staging area, local repository, upstream repository, and the commands associated with each (with explanations).
* Both resources are also available in other languages e.g. Spanish, French, and more
* "[Happy Git and GitHub for the useR](http://happygitwithr.com)" is an accessible, free online book by Jenny Bryan on how to setup and use git and GitHub with specific references on the integration of git with RStudio and working with git in R.
