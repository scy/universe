FROM debian:wheezy

MAINTAINER Tim Weber <scy@scy.name>

# Start me up like this:
#   docker run -d --name samba -v /srv/permanent:/srv/permanent -v /srv/volatile:/srv/volatile -p 139:139 -p 445:445 scy83/samba
#
# Then, if you're running this for the first time, create a password for "scy":
#   docker exec -ti samba smbpasswd -a scy

RUN apt-get update                                                        && \
    printf 'Apt::Install-Suggests "0";\nApt::Install-Recommends "0";\n'      \
           >/etc/apt/apt.conf.d/70nosuggests                              && \
    apt-get -y install samba samba-common-bin                             && \
    groupadd -g 1000 data                                                 && \
    useradd -c 'Tim Weber' -u 1000 -g 1000 scy                            && \
    useradd -c 'File Server Data' -u 3000 -g 1000 data                    && \
    mkdir /srv/permanent /srv/volatile /srv/test                          && \
    chown data:data /srv/permanent /srv/volatile /srv/test                && \
    chmod 0775 /srv/permanent /srv/volatile /srv/test                     && \
    echo 'It works!' >/srv/test/itworks.txt

COPY smb.conf /etc/samba/

# Default SMB ports.
EXPOSE 139 445

# Start smbd only (I'm not interested in nmbd support at the moment).
CMD ["/usr/sbin/smbd", "-FS"]
