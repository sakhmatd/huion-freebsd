# huion-freebsd
A system service to make the Huion H420 graphical tablet functional on FreeBSD.
May work with other Huion devices, let me know if it does.

# How To Use

To use the service, copy it to the service folder:

```
# cp huion /usr/local/etc/rc.d/
```

Add the service to rc.conf:

```
# sysrc huion_enable=YES
```

Then, either reboot, or start the service with
```
# service huion start
```

Make sure CUSE and Webcamd are enabled in your system.

Find the ugen for the tablet via `usbconfig`, then
create the appropriate devices with webcamd. Substitute the appropriate ugen for
your system:
```
# webcamd -B -d ugen1.5
```

The tablet should now function properly.

# How It Works

FreeBSD and moused in particular detect the tablet as a USB mouse by
default, creating a /dev/ums device. Since the tablet is not a USB
mouse, however, this does not work and it prevents webcamd from
attaching to the tablet properly.

This service adds a USB quirk that prevents FreeBSD from creating
the broken /dev/ums device.

Since the quirk is added via vendor ID, it is possible that
this would work for other Huion devices.

# License

Copyright 2021 Sergei Akhmatdinov

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
