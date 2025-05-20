# huion-freebsd
A system service to make the Huion graphical tablets functional on FreeBSD.

Confirmed to work with:
* H420
* H950P
* H952 (thanks to [@tingox](https://github.com/tingox))
* Kamvas 20 (thanks to [@sterentev](https://github.com/sterentev))

May work with other Huion devices, let me know if it does.

# How To Use

Make sure CUSE and Webcamd are enabled in your system.

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

# How It Works

FreeBSD and moused in particular detect the tablet as a USB mouse by
default, creating a /dev/ums device. However, since the tablet is not a USB
mouse, this does not work and it prevents webcamd from
attaching to the tablet properly.

This service adds a USB quirk that prevents FreeBSD from creating
the broken /dev/ums device.

Since the quirk is added via vendor ID, it is possible that
this would work for most Huion devices. 

# License

Copyright 2025 Sergei Akhmatdinov

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
