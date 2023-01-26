FROM ubuntu:22.04

LABEL maintainer="DevCel@protonmail.com"
LABEL description="Image for Linux Exploitation and Privilege Escalation Section - Task 1"


#################################### STANDARD STEPS ################################
# update
RUN apt update

# install ssh server
RUN apt install  openssh-server sudo -y

# install text editors
RUN apt install vim -y
RUN apt install nano -y

# add a user 'pupil' with credentials 'cla2023'
RUN useradd -ms /bin/bash pupil
RUN echo "pupil:cla2023" | chpasswd

# run the sh server and expose port 22
RUN service ssh start
EXPOSE 22


################################## TASK SPECIFIC ###################################

# create a flag for the to find
RUN echo "cla{y0u_h4v3_d0n3_w311}" > /root/flag.txt

# add a new user 'elliot'
RUN useradd -ms /bin/bash elliot
RUN echo "elliot:mrrobotisprettyneat" | chpasswd

# allow all users to look inside of it
RUN chmod 775 /home/elliot

# make the cp command a SUID
RUN chmod u+s /bin/cp



CMD ["/usr/sbin/sshd","-D"]


