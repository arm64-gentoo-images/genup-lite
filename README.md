# genup
Tool to update the **Portage**(5) tree, and all installed packages, under Gentoo Linux.

## Description
**genup-lite** is  a  utility  intended  to  simplify the process of keeping your Gentoo system up to date.  When invoked, it automatically performs the following steps, in order:
* updates Portage tree (and active overlays), and syncs **eix**(1)
(using `eix-sync`)
* removes any prior **emerge**(1) resume history
(using `emaint --fix cleanresume`)
* ensures **Portage**(5) itself is up-to-date
(using `emerge --oneshot --update portage`)
* updates all packages in the @world set
(using `emerge --deep --with-bdeps=y --newuse --update @world`)
* rebuilds any packages depending on stale libraries
(using `emerge @preserved-rebuild`)
* updates any old perl(1) modules
(using `perl-cleaner --all`)
* updates any old python(1) modules
(using `python-updater`)
* resolves clashing config file changes (in interactive mode)
(using `dispatch-conf`)
* removes unreferenced packages
(using `emerge --depclean`)
* fixes missing shared library dependencies
(using `revdep-rebuild`)
* updates environment settings (as a precautionary measure)
(using `env-update`)

The **genup-lite** utility can be invoked in non-interative (default) or interactive mode (see the  **--ask**  option in the manpage).   Non-interactive  mode  is  suitable  for use in a scripted invocation, for example as part of a nightly **cron**(8) job.

Unlike its sister utility **genup**(8), **genup-lite** does not attempt to upgrade the kernel, making it suitable for use in an embedded context.

## Installation

**genup-lite** is best installed (on Gentoo) via its ebuild, available as part of the **sakaki-tools-lite** [overlay](https://github.com/sakaki-/sakaki-tools-lite).
