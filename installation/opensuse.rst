openSUSE
===============================
.. rubric:: Scope:

* Officially supported openSUSE Leap releases and Tumbleweed

.. note::

    Execute the commands below in a root shell or with with a preceding :command:`sudo`.

Package Installation
--------------------
Packages are available from the official repositories:

* **tlp** – Power saving
* **tlp-rdw** – optional - :doc:`/settings/rdw`

Install them either with your favorite package manager or the command: ::

    zypper install tlp tlp-rdw

*openSUSE Leap 15.4 and higher as well as Tumbleweed*

Uninstall the conflicting `power-profiles-daemon` package: ::

   zypper remove power-profiles-daemon

Service Units
-------------
To complete the installation you must enable TLP's service: ::

   systemctl enable tlp.service

You should also mask the following services to avoid conflicts and assure proper
operation of TLP's :doc:`/settings/radio` options: ::

   systemctl mask systemd-rfkill.service systemd-rfkill.socket

.. seealso::

    * FAQ: :ref:`Service units <faq-service-units>`
    * FAQ: :ref:`faq-ppd-conflict`

ThinkPads only: External Kernel Modules
---------------------------------------
.. include:: ../include/thinkpad-kernel-modules.rst

Depending on your model and kernel version external kernel module(s) are required
to provide battery charge thresholds and recalibration.

For openSUSE `Tumbleweed` and  ThinkPads as of model year 2011 just install the
required external kernel module `acpi_call` from the official repositories with: ::

    zypper install acpi_call-kmp-default

For openSUSE `Leap` and/or older ThinkPads your mileage may vary as you have to
browse `openSUSE Software <https://software.opensuse.org/>`_ for community
packages or build the required module from source. The output of :command:`tlp-stat -b`
will guide you which external kernel module is required:

* **acpi_call** – optional – External kernel module providing battery
  recalibration for ThinkPads since model year 2011 - e.g. T420/X220 and newer
* **tp_smapi** – optional – External kernel module providing battery charge
  thresholds and recalibration for ThinkPads before model year 2011
  as well as specific :command:`tlp-stat -b` output until model year 2011

.. seealso::

    * Refer to :ref:`faq-which-kernel-module` for details
