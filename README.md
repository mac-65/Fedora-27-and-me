# Installing A Working Fedora 28 x86_64 Release

I have been using Fedora for quite some time.  It was my first Linux distro as far back as Fedora 8.  Recently, I wanted to upgrade to the latest version of Fedora, at the time of this writing, which is Fedora 31 (KDE Plasma 5.17.5).  I'm a KDE fan, and I have been using it since Fedora 8.

### Preamble

I have been using an older version for some time, and it was beginning to show its age with missing security patches and outdated tools.  In my old Sun Sparc workstation days, you never installed a binary _anything_.  You built the tool/library that you needed from source and installed it either in /use/local/\* or /opt or where ever you wanted.  Packages were tar source files.  But as software became more complex, pre-built packages became the norm.  An managing the dependencies between these packages and their versions suddenly exploded in complexity.  It was no longer just a matter (for the most part) of installing a binary package and "calling it a day."  That package might have dependencies on other packages that are not installed on your system, or installing that package may conflict with packages already installed on your system, or even that version of the package is incompatible with your system.

But, robust package managers were developed to handle these complex dependencies.  Additionally, the package itself could no longer be a simple collection of "things" to just install at their target location(s).  This packaging _format_ had to contain knowledge about its version and what dependencies and their versions were needed to complete a successful install.  This is contained in the package's metadata.  There are a bunch of different package formats available (https://en.wikipedia.org/wiki/Package_format) and RPM is the one Fedora uses along with yum/dnf as the framework to manages those package interactions with the installed OS and other packages (installed or dependant) on the system.

Anyway, all of that long winded stuff was to provide the context of how complicated an OS installation can be.  Trying to figure out these dependencies and interaction between various packages is way, way too much to do by hand anymore (not impossible, but really, really impracticable).

### So, What's The "Big Deal" About Installing Fedora 28?

Well, it started when something I needed to do required a later version of a library.  Unfortunately, there was no easy upgrade path for that library on the current version of Fedora I was running -- too many upstream problems and those broke some things on the installed system.  So I decided to upgrade my Fedora version.  The version I picked (at that time) was Fedora 29.

The install was pretty uneventful, and I was kinda used to the KDE upgrade mindset by that time.  The basic stuff worked as expected -- of course, it should!  Until I tried to launch VirtualBox on a VM I had been using on my current version of Fedora.  Now I had been testing VirtualBox on this new Fedora 29 system for other __easy__ VMs, but this VM halted right away.  Google didn't help and I tried several iterations of rebuilding the VM from scratch, etc. and so on.  I tried building the version of VirtualBox that ran the VM on Fedora 29, but that was another hornet's nest.  Finally, in fustration (and because I needed the VM) I reverted the entire system back to the old Fedora version.  I chalked the whole thing up to a broken VirtualBox version and the 'net seemed to support that suspicion.

### The Incredible, Not Edible, VirtualBox And It's Amazing Snapshots

Later, I needed to upgrade again for something.  And this time I decided to bit the bullet and ensure the upgrade would work for what I needed.  This time I figured out all of the tools that were required and a sound way to test their functionality after an upgrade.
Here's the list of must-work in the upgrade:

- wine

  I found that wine was the first application to go.  While each successive Fedora's version of wine happily installed, none would run my acid tests.  I selected 4 windows programs that must complete without a fatal error in wine for that version to be accepted: 3DMark2001SE, 3DMark03, 3DMark05, and Lightsmark2008.  If all of these ran, then that version of wine was accepted.
- VirtualBox
- yum
- yumex

I also figured out (by looking at the Fedora repos (https://archives.fedoraproject.org/pub/archive/fedora/linux/releases/) for the version of the library which Fedora release I could start with.  I knew Fedora 29 was a no go, So I started at Fedora 25.

### Down With Forced Obsolescence

The wonderful package manager __yum__ was replaced by a very immature __dnf__ towards the EOL of Fedora 21.  Even though it was advertised as a  _replacement_ for yum, it lacked some capabilities that I had become dependant on and had different behaviour than the traditional yum.  Plus, I really liked the clean direct approach yumex provided for viewing packages.  There was no really good, compatible yumex replacement.  I didn't really like yumex-dnf or dnfdragora.
