FROM ubuntu:20.04
RUN apt-get update
RUN apt-get install ssh -y # make sure it works for selection country code
RUN service ssh restart
RUN mkdir -p /data
RUN chmod 701 /data
RUN groupadd sftp_users
RUN useradd -g sftp_users -d /upload -s /sbin/nologin sftp_usr
RUN echo "sftp_usr:sftp" | chpasswd
RUN mkdir -p /data/sftp_usr/upload
RUN chown -R root:sftp_users /data/sftp_usr
RUN chown -R sftp_usr:sftp_users /data/sftp_usr/upload
RUN echo "Match Group sftp_users" >> /etc/ssh/sshd_config
RUN echo "ChrootDirectory /data/%u" >> /etc/ssh/sshd_config
RUN echo "ForceCommand internal-sftp" >> /etc/ssh/sshd_config
RUN service ssh restart
CMD /bin/bash