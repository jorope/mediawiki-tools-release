Releasing
=========

makerelease2.py: A Handy-dandy tool to pull a tagged release out of Git and
generate:

* a tarball
* a patch to previous revision
* GPG signatures for the above

You will first need to install `git-archive-all`:

`pip install git-archive-all`

```
usage: makerelease2.py [-h] [--previous PREVIOUS] [--sign]
 [--output_dir OUTPUT_DIR] [--upload-tar UPLOAD_TAR] repository tag

positional arguments:
repository               Path to the MediaWiki git repository
tag                      Git tag (or branch) to archive

optional arguments:
-h, --help               show this help message and exit
--previous PREVIOUS      Previous tarball to create a patch against
--sign                   Sign the generated contents with GPG
--output_dir OUTPUT_DIR  Location to put tarballs, relative to current
                         directory
--upload-tar UPLOAD_TAR  Tarfile to put generated tarballs into
```
Example:

After you have created (and signed!) the git tag in your git repo, you can run
a command like:

```
makerelease2.py --sign \
                --upload-tar /tmp/upload.tar \
                --previous 1.27.4 \
                /path/to/mediawiki/core 1.27.5
```

This is will make a release for the 1.27.5 tag in the repo at
`/path/to/mediawiki/core`, create patches to the previous release 1.27.4 and
generate signature files for all the created files. It will then put all the
generated files in `/tmp/upload.tar` in a folder called `1.27`. You can reuse
this tar to put numerous different MediaWiki releases for upload to the
releases server.

Branching
=========

Using branch.py to create a new wmf production branch for the MediaWiki train:

```
./branch.py --core \
            --core-bundle wmf_core \
            --bundle wmf_branch \
            --branchpoint origin/HEAD \
            --core-version <VERSION>
```