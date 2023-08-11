# Synctal

This is just a single-file bash script for simple two-way sync.  First passed
argument is the client-side directory and second passed argument is the
server-side directory, as you would type it into rsync.
Ex. synctal ~/mydirectory andrew@192.168.1.110:/home/andrew/mydirectory.

Quick note:  If you use this incorrectly, you *can* completely wipe the
directory.  (See explanation of "*Very* important usage note" below.)  Just be
careful.

The primary purpose here is to replace Unison because Unison's dependency
hell, incompatibility between versions, and the requirement that both client
and server have it installed makes it impossible to use in the majority of
situations that I find myself in.

I looked at Syncthing briefly, but having to use a browser interface just
seems annoying (and probably not safe).  Plus it actually does way more than I
need.

Synctal is only needed in the client.  Synctal is pure bash, so it should run
out-of-the-box without any problems in any *NIX environment that has the Core
GNU Utils installed (and maybe Busybox, but I don't know about that).  It's
written with Desktop Linux, Termux, Raspberry Pi, and WSL in mind.

It does, though, have the following dependencies: ssh, rsync, find, grep,
sort, and diff.
I don't know any Linux system that does *not* have those apart from the
Android Terminal Emulator (which is why I use Termux).

One major disadvantage that this has against Unison is that this does
not currently handle conflicts, and probably never will.  There also may be
other features that Unison has that this doesn't that I don't know about.

This is really just something I slapped together to sync a directory on my
phone with my desktop, so don't expect too much.  I'm not currently willing to
use this on files I'm not willing to risk losing

The actual moving of files is done by rsync over ssh.  If something other than
ssh needs to be used or if the port needs to be changed, then the script can
be altered easily enough.

Be sure to include the final slashes when describing directories!  You know
how weird rsync can be.  Or maybe you don't.  If you don't know, rsync can be
weird.

*Very* important usage note:  If a directory has already been synced before
*and* you decide to sync it again to a different directory (presumably one
that's empty), everything will be deleted!  That's because it will think the
remote has deleted everything.  If you need to re-sync from scratch, delete
the .synctal-list file.  And you'll also want to rarely, if ever, directly
call synctal from the terminal.  Better to dump it into a script first to make
sure you're always calling the same thing.
