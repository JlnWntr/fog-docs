.. include:: /includes.rst

----------------------------
Change FOG Server IP Address
----------------------------

Procedural Steps
================

- Follow appropriate steps for your Linux distribution to change the OS's IP address.
- Update the ipaddress= field (and other fields if necessary) inside the /opt/fog/.fogsettings file. :ref:`More information about the fogsettings file <install_fogsettings>`.
- Rerun the installer, you'll need to use **--recreate-CA** and **--recreate-keys keys** as the installer provides a certificate with a Common Name based on the ip which will be shipped in the iPxe kernel and failed to load any https resources as the certificate isn't valid anymore.
- Update the IP address inside ``/tftpboot/default.ipxe`` (look for the chain line i.e ``chain https://x.x.x.x/fog/service/ipxe/boot.php##params``)
- Update the IP address for the storage node on the FOG system where you changed the IP address Web Interface -> Storage Management
- Update the IP address on a any master storage node that may reference this FOG server Web Interface -> Storage Management
- (For master server) Update the FOG_WEB_HOST value Web Interface -> FOG Configuration -> FOG Settings -> Web Server -> FOG_WEB_HOST
- (For master server) Update the FOG_TFTP_HOST value Web Interface -> FOG Configuration -> FOG Settings -> TFTP Server -> FOG_TFTP_HOST

Optionaly if you have configured a dhcpd:

- Update IP addresses (fog and gateway) inside the ``/etc/dhcp/dhcpd.conf``.
- Don't forgot to check your ``/etc/export`` for nfs server as well as your apache2 configuration as the installer override it.
