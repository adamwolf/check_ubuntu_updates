check_ubuntu_updates
====================

Introduction
------------
`check_ubuntu_updates` is a collection of Nagios plugins for checking if an Ubuntu system has package updates.

`check_ubuntu_update_notifier` checks the same thing that the default shell does upon login.  It splits the updates into security updates and non-security updates.  It has Nagios-style warning and error thresholds, and separate thresholds can be set for each.

`check_ubuntu_requires_reboot` checks to see if the system reports that it requires a reboot due to updates.  It either emits OK or not, and has no configuration.

Installation
------------
Copy `check_ubuntu_update_notifier` and `check_ubuntu_requires_reboot` to the Nagios client, and run the script via remote execution from your Nagios server.

`check_ubuntu_update_notifier` requires Python, but unless you have an unusual Ubuntu system, this should be already set up.

Configuration
-------------
`check_ubuntu_require_reboot` has no configuration options, but `check_ubuntu_update_notifier` does.

```
./check_ubuntu_update_notifier -h
usage: check_ubuntu_update_notifier [-h] [-w WARNING] [-c CRITICAL]

Use /usr/lib/update-notifier/apt-check to check for number of updates (and
security updates) on a system.

optional arguments:
  -h, --help            show this help message and exit
  -w WARNING, --warning WARNING
                        Emit a warning if count of updates or security updates
                        is greater than this threshold. Format is
                        UPDATECOUNT,SECURITYUPDATECOUNT
  -c CRITICAL, --critical CRITICAL
                        Emit a critical state if count of updates or security
                        updates is greater than this threshold. Format is
                        UPDATECOUNT,SECURITYUPDATECOUNT.
```

Roadmap
-------

* Make sure check_ubuntu_update_notifier runs on Python 3.

Testing
-------
At this point, I have linters set up, but no automated tests.

To run `tests/lint`, make sure that you have shellcheck and flake8 installed.  `tests/ci` will create a virtualenv and install flake8 into it, but you have to have virtualenv installed.

`tests/lint` is meant to be run from the root of the project directory.
`tests/ci` is meant to be run from the root of the project directory.
