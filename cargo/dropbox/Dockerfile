FROM debian:wheezy

MAINTAINER Tim Weber <scy@scy.name>

# Download the client.
ADD https://www.dropbox.com/download?plat=lnx.x86_64 /tmp/dropbox.tar.gz

# Add a user, allow them to access the tarball and install required packages.
RUN useradd -c Dropbox -s /bin/bash -U -m dropbox && \
    chown dropbox:dropbox /tmp/dropbox.tar.gz     && \
    apt-get update                                && \
    apt-get -y install lsb-release python-gpgme

# Do everything else as a non-privileged user.
USER dropbox

# Extract the client.
RUN ["/bin/sh", "-c", "cd && tar xzvf /tmp/dropbox.tar.gz"]

# Start it.
CMD ["/home/dropbox/.dropbox-dist/dropboxd"]
