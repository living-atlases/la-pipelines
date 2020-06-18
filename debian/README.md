## Intro

## Prerequisites

```
sudo apt install debhelper
sudo apt install devscripts
```

## Build

You can generate a non-signed debian package via:

```bash
debuild -us -uc -b
```
in the parent of this directory. This will generate the deb file in the parent directory of this repository.

You can increase changelog version and comments with `dch` utility, like with `dch -i` that increase minor version.

Add to your .gitignore:
```
*/*.debhelper
*/*.debhelper.log
*.buildinfo
*.substvars
debian/files
debian/la-pipelines
```

## Using systemd?

Just create here your systemad service like
debian/la-pipelines.service
debian/la-pipelines.conf

see ala-images debian package for details

## Looking for inspiration?

You can see [tomcat7-examples package source](https://salsa.debian.org/java-team/tomcat7/tree/master/debian) for inspiration of tomcat7 packages and also about how to create multiple debian packages from a same source repository.

Also `dbconfig-common` package have some samples in `/usr/share/doc/dbconfig-common/examples/` for mysql and postgresql debian configuration tasks for packages.

## Testing

You can test the generated package without install it with `piuparts` like:

```bash
sudo piuparts -D ubuntu -d xenial -d bionic ../la-pipelines_1.0-SNAPSHOT_all.deb
```
in this way you can also test it in different releases.

Read `/usr/share/doc/piuparts/README.*` for more usage samples.

