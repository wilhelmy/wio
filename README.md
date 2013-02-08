Welcome WIO Editors!
--------------------

This is the new and improved www.irchelp.org.

PLEASE be aware that this is not a normal open source project, but rather the files that comprise a website being
ran as a public service. 
No right to redistribute these files is granted, but you may use them for the purpose of making improvements and
submitting them back to us. See COPYING for more information.

Otherwise, please do not create mirrors of the site, thanks.


Directory Structure
-------------------

 * documents/ - contains the files that will be processed as input by PieCrust
 * * documents/_content/pages - contains source used to generate HTML pages
 * * documents/_content/posts - contains blog posts (will eventually be used for site news. unused for now)
 * * documents/_content/templates - contains the page template parts of the site theme
 * * documents/media/ - contains images and PDFs that are included in our documents.
 * * img/ css/ js/ - contain the static parts of the site theme.
 * * documents/.htaccess - contains lots and lots of redirects. Whenever you move a page, you should add a redirect here.
 * otherfiles/ - contains other files that are not directly included in the site
 * _piecrust/ - contains a copy of _piecrust downloaded as described below.


Build Process
-------------

The build process should eventually go something like this.

 1. a _counter folder is created in documents
 2. the documents folder is processed with PieCrust and the output placed in
    the root of _counter
 3. Sanity checks are optionally performed (has the size dropped more than it should,
    etc)
 4. Entire contents of target are rsynced to a staging folder on the server.
 5. The live folder is renamed to old, and the staging folder is renamed so
    that it becomes the live folder.

Getting PieCrust
----------------
*Note: This is only necessary to run the development server, or to compile the site.*
*There is no need to download PieCrust just to make changes to content, although it may make it easier to preview your change.*

Run this command from the root of your wio git repository.

	hg clone https://bitbucket.org/ludovicchabant/piecrust _piecrust


Running the Development Server
------------------------------

After downloading PieCrust as described above, run the serve_devsite.sh script
from the root of your wio git repository:

	./serve_devsite.sh

This will run a testing server that you can connect to via http://localhost:8080,
which will update automatically as files are changed in the documents
folder. The testing server remains attached to the terminal and can be ended
with ctrl+c when done testing.

This differs slightly from the production setup, in that the production
setup requires the site to be built (see below)  before it's uploaded to the server.

The development server does not automatically find an index.html file in the current folder as
Apache would, so relative links such as /irchelp/clients/ will display an error. Simply add index.html
to the end of the URL.

The development server also does not read the .htaccess file and therefore will not redirect.

Building the Site
-----------------

	./bake_site.sh

Publishing the Site to Staging
------------------------------

 * Currently done manually by running the build steps on the development server. 
 
Publishing the Site to Production (Live Site)
---------------------------------------------

 * Not implemented yet. A branch or seperate production repository with regular pushes from the development tree
 will likely be used.


Authoring Documents for www.irchelp.org
---------------------------------------
*This is an early draft of this guide, documenting the new way we're going to maintain www.irvhelp.org.*

## Introduction

This site is run by a group of volunteers primarily consisting of the ops from the #irchelp channel on EFNet. We welcome contributions to the site, but have a number of guidelines which you should
follow so that your content can be easily included into the site.


## Site Migration Information

The latest migration news and information can be found [here](migration.html).


## Technical Information

As of 2012, all content on the site is maintained as Markdown files (which *should* have a short YAML header containing metadata). [Markdown](en.wikipedia.org/wiki/Markdown) is a simple way of adding formatting to text files, very similar to wiki markup.

   The files are kept in a [Git](http://git-scm.org) repository, and automatically generated using [PieCrust](http://bolt80.com/piecrust/).

The Git repository is very important to this process - it's the part that will allow multiple editors access to update the site, without risk of stepping on each other's toes, and which will allow us to easily roll back unwanted changes.

### Document Header (YAML Front Matter)
The document header is written in YAML, and delimited with three dashes. It is a simple list of name: value pairs that describe each document. These header are available as variables to be used in templates.

A sample header follows:

	---
	title: Document title
	author: random-irchelper
	datecreated: 1 September 1993
	dateupdated: 30 November 2012
	status: (this is optional, but I'm going to add hooks that put a warning message about depreciated content if the status is "historical")
	summary: This is a summary.
	---

Note the --- at the beginning and end of the header. This seperates the header from the content, and is required for PieCrust to recognize this as a header. The header is **not** Markdown formatted, so most other Markdown parsers will not format it.


## Useful tools

Several programs are useful to irchelp.org authors.

  * [retext](http://sourceforge.net/p/retext/home/ReText/) is a graphical editor with live preview for Linux systems (available in the Ubuntu repositories as *retext*).
  * [PieCrust](http://bolt80.com/piecrust/) is useful to be able to test the automatic build process, but not required for authors.
  * [Git](http://git-scm.com/) is necessary to read/write the repository which stores the source to the website. Clients are available there for virtually all operating systems, not just Linux :)
  * Your favorite text editor. Most programming-oriented text editors, such as vim, emacs, and others have syntax highlighting for Markdown, but any text editor will do, since the files are just text.




## Content Guidelines
  * We are not a software hosting site. No executables or archive files will be hosted - links should be provided to landing pages for stable and canonical download locations for any software mentioned on the site.
  * We are aiming to be as network-agnostic as possible. In the past, IRCHelp.org was EFNet and IRCNet centric, we are in the process of changing that.

## Legal Requirements

Going forward, in order to protect ourselves from any legal trouble and avoid having to scramble to remove articles, we need to have clear rights to use all content on irchelp.org. Third parties are asked to give a clear grant of rights.

This can take one of two forms - the content may be generally licensed under terms that permit anyone to use it - public domain or an acceptable free documentation license, or the content may be provided to irchelp.org under a release that grants us a non-revocable right to publish it, and if necessary, maintain it. 
  
### Acceptable Licenses

A non-exhaustive list of licenses that are sufficient for us to be able to publish third-party content.

  * CC-BY
  * CC-BY-SA
  * GFDL
  * Public Domain
  * Others?
  
A license which does not permit derived works is not sufficient, as we need to be able to maintain current information.  (this includes CC-BY-ND or CC-BY-NC-ND) 

* * *


