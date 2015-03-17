FROM debian:wheezy

MAINTAINER Tim Weber <scy@scy.name>

# Run me like this:
#   docker run -d --name dropbox -v /srv/permanent/Dropbox:/home/dropbox/Dropbox scy83/dropbox
# Then, check
#   docker logs -f dropbox
# for the URL to allow access.

# Download the client.
ADD https://www.dropbox.com/download?plat=lnx.x86_64 /tmp/dropbox.tar.gz

# Add a user, allow them to access the tarball and install required packages.
RUN useradd -c Dropbox -s /bin/bash -U -m dropbox && \
    chown dropbox:dropbox /tmp/dropbox.tar.gz     && \
    apt-get update                                && \
    apt-get -y install lsb-release python-gpgme   && \
    echo fs.inotify.max_user_watches=100000 >>/etc/sysctl.conf

# Do everything else as a non-privileged user.
USER dropbox

# Extract the client.
RUN ["/bin/sh", "-c", "cd && tar xzvf /tmp/dropbox.tar.gz"]

# Start it.
CMD ["/home/dropbox/.dropbox-dist/dropboxd"]
