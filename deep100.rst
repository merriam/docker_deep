Docker Extension/Expansion Proposal:  URIs to replace docker commands

I am thinking that this might be an interesting enhancement, and would love comments before writing any code.

DEEP:                  number tbd
Title:                   URIs to replace docker commands
Last Modified:     Sun Dec 22 16:18:35 PST 2013
Author:               Charles Merriam <charles.merriam@gmail.com>
Status:                Proposed
Content-Type:	text/x-rst
Created:	           22-Dec-2013
Docker-Version:	0.7.2

-------

Contents
--------

    1.  Abstract


Abstract
--------

Working with filesystems in Docker requires many different commands including  import, export, load, save, insert, and cp.  These command each have separate syntax and no clear pattern.   The expansion tries to make the syntax easier to remember and read, and perhaps, to implement.   Some commands would change to allow an expanded URI syntax [http://en.wikipedia.org/wiki/URI_scheme].  Currently, Docker commands such as insert and cp only accept "http://website.tld/path" and "https://website.tld/path".   After this expansion, these command would also accept "file:path", "tar:path", "container:id[/path]", "image:id[/path]".  It would also accept shorthand of "c:" for "container:" and "i:" for "image:".

Examples
---------

    These are before and after examples of the File Systems section of the Docker Quick Reference Card [http://charlesmerriam.com/docker/quick_docker.html]

    Description                                       Current Command                         Proposed Command
    ====================       ===================      ====================


    Create a new image from a local tar file.
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    $ docker import - < a6ef_files.tar
    $ docker import server.com/files.tar charlesmerriam/dwarf:in_progress

    becomes:

    $ docker cp tar:a6ef_files.tar image:
    $ docker cp tar://server.com/files.tar i:charlesmerriam/dwarf:in_progress

    Copy filesystem from container
    ~~~~~~~~~~~~~~~~~~~~~~~~~

    $ docker export a6e5 > a6e5_files.tar

    becomes:

    $ docker cp container:a6e5 tar:- > a6e5_files.tar
    $ docker cp c:a6e5 tar:a6e5_files.tar

    Create a new image from a remote tar file
    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

    $ docker import - < a6ef_files.tar
    $ docker import server.com/files.tar charlesmerriam/dwarf:in_progress

    becomes:

    $ docker cp tar:a6ef_files.tar image:
    $ docker cp tar://server.com/files.tar i:charlesmerriam/dwarf:in_progress








The change is in the URI syntax accepted.  Currently, only "http:/
I've been playing with Docker for a little bit and find some of the commands cumbersome. t  Looking at the Quick Reference (http://charlesmerriam.com/docker/quick_docker.html), we see these types of commands:

     $ docker import http://foobar.com/myfiles/foo.tar REPO:TAG
     $ docker export CONTAINER   # to stdout tar file
     $ load source.tar
     $ save IMAGE  # to stdout tar
     $ insert IMAGE http://foobar.com/myfiles/afile.txt
     $ cp CONTAINER:path localpath

The URLs mentioned are only "http://" or "https://".   I propose expanding the URIs recognized by Docker and replace the above lines with:

      $ docker cp http://foobar.com/myfiles/foo.tar repo://REPO:TAG
      $ docker cp cont://CONTAINER tar:-
      $ docker cp

So the new URI syntax would be:


Copyright
----------

        This document is placed in the public domain
