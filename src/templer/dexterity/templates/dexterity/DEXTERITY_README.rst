Congratulations! If you're reading this document, you have created a Python
package meant to support development of Dexterity content types and behaviors.
This document introduces you to use to the package skeleton.

Adding the package to your Plone installation
=============================================

You have probably created this package in a ./src subdirectory of your
buildout directory. If not, you may wish to move it there. The ./src
subdirectory is the expected place for development packages, and
development tools and documentation often assume this location.

Creating a development package does not automatically add the
package to your Plone runtime environment.

To do so, first find the
"eggs =" section of your buildout and add the name of
this package to your egg list::

    eggs =
        Plone
        Pillow
        lxml
        plone.app.dexterity
        ...
        ${namespace_package}.${package}

Next, you must tell buildout how to find the package. Otherwise, it would try
to download the package from a package repository. Look for the "develop ="
section of your buildout configuration file and add the path to this package::

    develop =
        src/${namespace_package}.${package}

Alternatively, you may use mr.developer to add the development package.

Now, run bin/buildout to integrate the new package into your runtime
environment. Restart zope/plone. Note that you should nearly always
use "foreground" mode when developing a package.

Adding Content Type and Behavior Skeletons
==========================================

You may use Templer and templer.dexterity to add content type or behavior
skeletons to your package. To do so, you must first integrate the new
package into your runtime environment (as described above) and run
buildout. Without that step, you will not be able to use the "add"
command.

The "add" command allows for addition of "sub" skeletons like
content types and behaviors. It must be run inside the "src"
directory of this package using the "paster add" command.

To get a list of available add commands, do the following,
starting from your buildout directory::

    cd src/${namespace_package}.${package}/src
    ../../../bin/paster add --list

To add a new content type skeleton::

    cd src/${namespace_package}.${package}/src
    ../../../bin/paster add content_type

And, a behavior::

    cd src/${namespace_package}.${package}/src
    ../../../bin/paster add content_type

As when you ran templer to create this package, templer will
ask you the questions that must be answered to create the
new skeleton.

Guide to the package skeleton
=============================

Guide to content type skeletons
===============================

Content Type testing
--------------------

Guide to behavior skeletons
===========================

Behavior testing
----------------


Before Package Distribution or Deployment
=========================================

You should delete this file from your package before package distribution.
Failure to do so may result in your being ridiculed.

In order to support local "add" commands, Templer created Paste,
PasteDeploy and PasteScript eggs inside your product. These are only needed
for development. You can and should remove them from your add-on distribution.

Also remove::

  setup_requires=["PasteScript"],
  paster_plugins=["templer.localcommands"],

from the packages setup.py.
