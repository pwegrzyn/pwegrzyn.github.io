---
authors:
- name: "Patryk Węgrzyn"
date: 2020-09-14
linktitle: Software migration tips 
type:
- post 
- posts
title: Software migration tips (Python 3 edition)
weight: 1
categories:
- python
- software
---

**In this post I'd like to share some tips in regard to migrating a fairly complex software system to a new version
of the programming language in which it has been originally written in. Most of the advice will be based on and related to the migration
from Python 2 to Python 3 as this is probably the most likely migration process you can encounter in your near-future software career and it also happens to be
the process I have the most experience with.** 

Preparation
--------
Migration can be a really daunting, complex and filled-with-traps process. Therefore it's crucial to properly prepare for what's to come. You should take some
time to prepare a full plan for the migration process with more-or-less strict deadlines that'll keep you productive and focused on track. Try to read about what
are the most imporant changes between the new and old version. Make sure you understand the mechanisms and ideas behind all implementation details of the legacy version.
Read blogs posts, watch videos and do whatever it takes to learn how to migration process was conducted in other companies/teams and try to reflect it onto your system.

Don't underestiamte the challange
--------
You might think that a migration is relatively simple task doable within a couple of days. In some cases, where the system is simple, well structured, non-complex and has lot's
of tests already written that might as well be true. But in general, if the system is more complex and especially if it has some technical debt and/or depends heavily on implementation
details that become fundamentally broken/changed after the migration, you should be allocate at least a couple of months for the migration even have the slightest chance of being successfull. You know, just assume that THERE WILL BE PROBLEMS - there will be situations in which spend hours debugging what's wrong just for it to turn out that the implementation
of a single function for database interactions has introduced a tiny side effect in the new version.

Spend time understanding the internals
--------
If the system is complex take, take your time and try to understand most of the critical sub-parts of the system, so that during the migration you already know what can brake and how to fix it. This is especially important if you are a new member in the new, or the team itself got created just for the purpose of migration.

Split the process
--------
In general, be prepared to migrate the system part-by-part, not all at once. Debugging would be a nightmare if you could not trust ANY part of your system. But migration one component
at a time you can steadily progress the process and build on top of already working sub-parts.

Automate as much as possible
--------
Try to use already existing tools which automate the boilerplate parts of the migration. In the case of Python, there are tools like *2to3* and *six*, which take care of automatically applying simple syntax changes, standard library module paths, function signatures, etc. I'd adivce to split this process and apply these *fixers* (as they are called) ony by one, since doing it at once can lead to subtle bugs which can be hard to debug later on.

Test, test, test
--------
If your system already has a proper amount of tests then you're in luck. Otherwise a good idea would be to prepare unit tests before the migration process, make them pass on the old oversion and then start the migration but with the requirement that at all time the old unit tests must continue to pass.

Implement fallback mechanisms
--------
The new version will have bugs, deal with it. Always have available methods to fallback the the old version if things go bad on production. The mechanisms themselves should be well tested and able to swtich the implementation quickly, easily and painlessly.

Be ready to come up with clever ideas
--------
The migration might introduce problems which will be highly non-trivial and will require lots of creativity to solve. From experience I can say that if you have some sort of object serialization in your project (using *pickle* or any other module) in Python 2 and you want to port it to Python 3 (while preserving data compatiblity) then you are pretty much screwed, and getting out of this situation will require lots of creative thinking ;-).

Consider upgrading your dependencies
--------
A migration might be a good time to finnaly update some of you super-old dependencies. This will be a security and maintainability win for all. This decision might as well be forced on you, since the old version of your software may have dependencies to specific version of libraries which are no longer maintained or are not compatible with your new version.

Don't overestimate your ability to introduce massive refactoring
--------
The migration by itself will be a huge undertaking, don't make it harder for yourself and adding massive refactors on top of it. Stuff like adding type-hinting in Python, moving from a custom WSGI application to Django, rewritting logging mechanisms - sure, these all sound nice, but you can always come back to them after the migration is finished.

Bonus: Python 2->3 specific issues
--------
Here are some the most imporant things to keep in mind when in comes to migrating to Python 3:
* distincation between raw, C-like bytes and decoded strings
* order of dict and set elements is random and you should not depend on it
* syntax changes: handling exception, print-keyword, etc.
* ```.has_key()``` is replaced by ```in```
* modules implemented in C, like cString become the default
* some modules in the standard library are renamed or moved (e.g. httpclient)
* ```psycopg2``` uses ```bytearray``` (not ```bytes```!) as the default type for BYTEA attributes
* ```pickle``` was massively changed in Python 3 - compatibility with Python 2 is possible but is super tricky

Conclusion
--------
That's it for today, thanks for reading. I'll try to update this post if some other tips come to my mind at some point in the future.
