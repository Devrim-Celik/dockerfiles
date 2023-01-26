FROM ubuntu:22.04

LABEL maintainer="DevCel@protonmail.com"
LABEL description="Image for Linux Exploitation and Privilege Escalation Section - Task 3"


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
RUN echo "cla{100k_w17h1n_y0u}" > /root/flag.txt

# add a new user 'elliot'
RUN useradd -ms /bin/bash elliot
RUN echo "elliot:mrrobotisprettyneat" | chpasswd
RUN chmod 775 /home/elliot

# install python
RUN apt install python3 -y

# add a python script 
ADD random_message.py /home/pupil/random_message.py
RUN chmod 744 /home/pupil/random_message.py

# give permission to pupil
RUN echo "pupil ALL=(root) /usr/bin/python3 /home/pupil/random_message.py" >> /etc/sudoers



CMD ["/usr/sbin/sshd", "-D"]


