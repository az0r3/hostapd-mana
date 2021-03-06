hostapd-mana
============

[![CodeBuild Build Status](https://codebuild.us-east-1.amazonaws.com/badges?uuid=eyJlbmNyeXB0ZWREYXRhIjoiVTZhaGZ1elVRUkozQkpHMDJFQm83VkNtTVBOK3FaTzZtYjJGM3dUM20razNrVjMxS1hlZEFCQjNxRmIycHdRNWZsQTJVeFJnUVJyc25JRU85NStNcUY0PSIsIml2UGFyYW1ldGVyU3BlYyI6Ik15cGlYdUtZQys2SkFzYVkiLCJtYXRlcmlhbFNldFNlcmlhbCI6MX0%3D&branch=hostapd-2.6)](https://s3.amazonaws.com/sensepost-hostapd-mana/binaries/hostapd-mana-ELF-x86-64.zip)
[![Travis Build Status](https://travis-ci.org/sensepost/hostapd-mana.svg?branch=hostapd-2.6)](https://travis-ci.org/sensepost/hostapd-mana)

## Bootstrap

### Be aware
This tool appears to be *extremely* sensitive to connection quality. Substantial hours were spent on debugging an error residing mostly in the real world.

### Steps
* Gen server cert presented to user:
```
openssl genrsa -out rootCA.key 2048
openssl req -x509 -new -key rootCA.key -out rootCA.crt
openssl x509 rootCA.crt -out rootCA.pem

openssl genrsa -out user.key 2048
openssl req -new -sha256 -key user.key -out user.csr
openssl x509 -req -in user.csr -CA rootCA.crt -CAkey rootCA.key -CAcreateserial -out user.crt -sha256
openssl x509 user.crt -out user.pem
```
* Set up iface/SSID/channel @ example.conf
* `$ make -C hostapd -j8`
* `# hostapd/hostapd example.conf`

## Overview

A featureful rogue access point first presented at [Defcon 22](https://www.youtube.com/watch?v=i2-jReLBSVk) by Dominic White ([@singe](https://twitter.com/singe)) & Ian de Villiers @ sensepost (research@sensepost.com)

## Documentation

Check [the wiki](https://github.com/sensepost/hostapd-mana/wiki) for information of getting and using hostapd-mana.

## License

The patches included in hostapd-mana by SensePost are licensed under the BSD license. Permissions beyond the scope of this license may be available at http://sensepost.com/contact us/. hostapd's code retains it's original license available in [COPYING](https://github.com/sensepost/hostapd-mana/blob/master/COPYING).
