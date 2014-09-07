randrctl
========

Minimalistic profile based screen manager for X. It allows to store current screen setup in a declarative configuration file (a profile) and apply stored settigns later with a simple command.

Tool may be usefull to people who work on the same laptop at home, in the office (different external displays and different screen setup) and on the go (no external display).

Currently following features are suppoted
* dumping current screen setup to file
* listing available profiles
* displaying profile details
* switching between stored profiles
* running custom commands before/after switch

Usage is very simple:

1. Setup your screen to suit your needs and dump settings to use them later

  randrctl dump home

2. After this you can reapply these settings whenever you need them

  randrctl switch-to home
  
3. You can list all available profiles

  randrctl list
  
4. And if you are interested in some particular profile

  randrctl show home
  

Before/After hooks
------------------

Some window managers (i.e. i3) are known to crash when screen setup is changed. Common workaround for this is:

  killall -SIGSTOP i3
  xrandr ...
  killall -SIGCONT i3

randrctl handles this by allowing to declare hooks to be executed before and after call to xrandr. Declare them in /etc/randrctl/config.ini

  [hooks]
  before_apply = /usr/bin/killall -SIGSTOP i3
  after_apply = /usr/bin/killall -SIGCONT i3


Profile format
--------------

Simple JSON file. Can be edited by hand.

  {
    "outputs": {
      "LVDS1": {
        "width": 1366,
        "height": 768,
        "top": 0,
        "left": 0
      },
      "DP1": {
        "width": 1920,
        "height": 1080,
        "left": 1366
      }
    },
    "primary": "DP1"
  }


Upcoming features
-----------------

* detecting connected display and choosing the most appropriate profile (only opensource linux drivers allow this). There is a prototype already
* completion functions for popular shells
* per-user profiles and configuration (no need for su/sudo)


Feedback/contribution
---------------------

This is my very first python project. Comments regarding code quality and suggestions are welcome. 


License
-------
GPLv3