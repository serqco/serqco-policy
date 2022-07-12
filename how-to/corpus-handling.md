# How SERQco studies handle their corpora

created: Lutz Prechelt, 2022-07-12


## What is a corpus?

Most SERQco studies will use data from one or more yearly volumes
of one or more venues.
Each such volume is called a _corpus_ and contains 
one year of one journal 
(or of one recurring section or article type of a journal)
or one track of one year of one conference.

A corpus is a collection of PDF files, plus some metadata files.


## The problem

- A corpus is potentially fairly large.
  E.g. the overall ICSE ZIP distributions (including all tracks and
  workshops) for 2011 to 2021 have been in the range 0.3 to 1.0 GB.
- Files in a corpus will often have copyright limitations


## Storage platforms and limitations

GitHub repositories:

- https://docs.github.com/en/repositories/working-with-files/managing-large-files/about-large-files-on-github
- https://stackoverflow.com/a/59479166/ is even more informative.
- Repositories can be public or private.
- File size: above 50 MB creates a warning; pushes are limited to 100 MB.  
- Repo size: "ideally" under 1 GB; under 5 GB is "strongly recommended".  
- Corpus repos could even be attached to a study repo as git submodules,
  making handling relatively easy (at least in principle; in practice,
  git submodules are not fun.)
- Cloning a repo creates each contained file twice:
  Once in the repo, once in the working directory.
- Git LFS (Large File Storage) could avoid this, but
  GitHub LFS is size-limited to 1 GB per account -- not enough for SERQco.


GitHub Releases:

- https://docs.github.com/en/repositories/releasing-projects-on-github/about-releases
- Releases are based on a tag in a repo.
  They contain the repo snapshot represented by that tag,
  plus any number of manually added binary files.
- There are no size limits for releases.
- Can releases be private? Apparently not.


Nextcloud shared folders:

- Easy way to distribute a set of ZIP files that can handle multiple GBs.
- Can use password protection.
- Has a WebDAV API for scripted access:  
  https://docs.nextcloud.com/server/15/developer_manual/client_apis/WebDAV/basic.html  
  https://stackoverflow.com/questions/60936116/downloading-files-from-nextcloud-with-python-script-with-2-factor-authentication


## How SERQco studies handle their corpora

GitHub repositories and Nextcloud password-protected shared folders
both appear to be suitable.
Repos are a bit easier to handle (`git clone --recurse-submodoules`) 
if their size limitations are not a problem.

We will decide which we use when the corpus downloader is available and
we get to see actual corpus sizes.
