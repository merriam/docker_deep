*******************************************
DEEP 100 - URIs to Replace Docker Commands
*******************************************

- DEEP:                  100 (placeholder:  number tbd)
- Title:                   URIs to replace docker commands
- Last Modified:     Sun Dec 22 16:18:35 PST 2013
- Repo Link:           `deep100.rst <https://github.com/merriam/docker_deep/blob/master/deep100.rst>`_
- Author:                Charles Merriam <charles.merriam@gmail.com>
- Status:                 Proposed
- Content-Type:	text/x-rst
- Created:	           22-Dec-2013
- Docker-Version:	0.7.2

Contents
--------


#.  Abstract_
#.  Examples_
#.  Copyright_



Abstract
--------

Working with filesystems in Docker requires many different commands including  import, export, load, save, insert, and cp.  These command each have separate syntax and no clear pattern.   The expansion tries to make the syntax easier to remember and read, and perhaps, to implement by using `URIs <http://en.wikipedia.org/wiki/URI_scheme>`_ of "file", "tar", "container" and "image".



Examples
---------

    These are before and after examples of the File Systems section of the `Docker Quick Reference Card <http://charlesmerriam.com/docker/quick_docker.html>`_.

+------+--------------------------------------------+--------------------------------------------+
| Line |    Current Command                         | Proposed Command                           |
+======+============================================+============================================+
+   1  | `import - < a6ef_files.tar`                | `cp tar:a6ef_files.tar image:`             |
+------+--------------------------------------------+--------------------------------------------+
+   2  | `import server.com/files.tar`              | `cp tar://server.com/files.tar`            |
+      |    `charlesmerriam/dwarf:in_progress`      |   `i:charlesmerriam/dwarf:in_progress`     |
+------+--------------------------------------------+--------------------------------------------+
+   3  | export a6e5 > a6e5_files.tar               | cp container:a6e5 tar:- > a6e5_files.tar   |
+      |                                            |  *or*  cp c:a6e5 tar:a6e5_files.tar        |
+------+--------------------------------------------+--------------------------------------------+
+   4  |                                            |                                            |
+------+--------------------------------------------+--------------------------------------------+

* cp a6e5:/var/log .
* cp a6e5:var/log/dpkg.log dpkg
* ls to replace docker images, maybe ps?,
* rm and rmi merge?
* ls -l c:… replaces -notrunc
* ls -
* ls -l c:… replaces history?
* save e71d > e71d.tar

1.  Use local tar file to create new image.
2.  Use http or https address to create new tagged image
3.  Use container filesystem to create tar file.
    Note that "c:" is shorthand for "container:"
4.  Use remote tar file to create new image.

Currently, a blank url, `docker.com/io.txt` is assumed to be `http`.   Explicit `http://` and `https://` are allowed.

::

     $ docker import http://foobar.com/myfiles/foo.tar REPO:TAG
     $ docker export CONTAINER   # to stdout tar file
     $ load source.tar
     $ save IMAGE  # to stdout tar
     $ insert IMAGE http://foobar.com/myfiles/afile.txt
     $ cp CONTAINER:path localpath



Copyright
----------

        This document is placed in the public domain
