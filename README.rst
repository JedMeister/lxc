TurnKey LXC LinuX Containers - 1 host, multiple TurnKey apps
============================================================

TurnKey LXC simplifies downloading and deploying multiple TurnKey apps
side-by-side on the same host in securely isolated lightweight
containers while handling tricky details such as network routing.
`LXC`_ (AKA LinuX Containers) is the rising star lightweight
virtualization technology that powers Docker and other next generation
software deployment platforms.

Usage
-----

Creating a TurnKey LXC container is done by specifying ``turnkey`` as
the template when invoking ``lxc-create``, for example::

    # lxc-create -n CONTAINER_NAME -f CONFIG_FILE -t turnkey -- APPNAME [template options]

See the `Usage Documentation`_ for further details.

Features
--------

This appliance includes all the standard features in `TurnKey Core`_, and on
top of that:

- Includes `TurnKey LXC template`_:

    - Download and create a container of any TurnKey appliance.
    - Appliance version defaults to ``latest available``.
    - Insert specified inithooks.conf into container for preseeding.
    - Supports configuration of network link (e.g., br0, natbr0, none).
    - Supports configuration of apt proxy.
    - Verifies GPG signatures when available
    - Wrapper for lxc-destroy cleans up after container is removed
    - Supports LVM on TurnKey's default volume group 'turnkey'
    - Allows TurnKey Ansible appliance to manage LXC containers
    - Generic enough to be used on any LXC enabled distribution.

- Easily expose NAT containers services:

    - `nginx-proxy`_: Expose a containers web services to the network by
      creating an nginx site configuration to proxy all web requests
      (ports 80, 443, 12320, 12321, 12322) destined for a specific
      domain to the container on the corresponding ports.
    - `iptables-nat`_: Expose a containers non-web (e.g., SSH) service
      to the network by configuring iptables on the host to forward the
      traffic it receives on port X to the container on port Y.

- LXC appliance configurations:

    - Preconfigured network bridge interface (br0).
    - Preconfigured network NAT bridge interface (natbr0).
    - Preconfigured dnsmasq on natbr0 providing DHCP and DNS services.
      Containers can be referenced by hostname or hostname.local.lxc
    - Includes apt-cacher-ng, binding to br0 interface.
    - Includes TurnKey web control panel (convenience).
    - Includes example inithooks configuration for preseeding (convenience).
    - IP forwarding and control groups enabled.

- LXC limitations:

    - The LXC appliance cannot run in nested mode i.e. within an LXC container
      without additional configuration. This mode is not recommended for
      production systems because of security concerns.

Credentials *(passwords set at first boot)*
-------------------------------------------

-  Webmin, SSH: username **root**

.. _LXC: https://linuxcontainers.org
.. _TurnKey Core: https://www.turnkeylinux.org/core
.. _TurnKey LXC template: https://github.com/turnkeylinux-apps/lxc/blob/master/overlay/usr/share/lxc/templates/lxc-turnkey
.. _nginx-proxy: https://github.com/turnkeylinux-apps/lxc/blob/master/overlay/usr/local/bin/nginx-proxy
.. _iptables-nat: https://github.com/turnkeylinux-apps/lxc/blob/master/overlay/usr/local/bin/iptables-nat
.. _Usage Documentation: https://github.com/turnkeylinux-apps/lxc/tree/master/docs/usage.rst

