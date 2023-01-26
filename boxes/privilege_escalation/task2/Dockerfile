FROM ubuntu:22.04

LABEL maintainer="DevCel@protonmail.com"
LABEL description="Image for Linux Exploitation and Privilege Escalation Section - Task 2"


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
RUN echo "cla{7h3_71m3k33p32_100k5_up0n_y0u}" > /root/flag.txt

# add a new user 'elliot'
RUN useradd -ms /bin/bash elliot
RUN echo "elliot:mrrobotisprettyneat" | chpasswd

# install curl
RUN apt install curl -y
RUN apt install cron -y

# allow all users to look inside of it
RUN chmod 775 /home/elliot

# create a directory in the pupil home direct with books
#RUN mkdir /home/pupil/books
#RUN curl https://gist.githubusercontent.com/phillipj/4944029/raw/75ba2243dd5ec2875f629bf5d79f6c1e4b5a8b46/alice_in_wonderland.txt > /home/pupil/books/alice_in_wonderland.txt
#RUN curl https://raw.githubusercontent.com/cgovella/learning/master/edx-python/case%20studies/gutenverg/Books/English/shakespeare/Romeo%20and%20Juliet.txt > /home/pupil/books/romeo_and_juliet.txt
#RUN curl  https://raw.githubusercontent.com/gjtorikian/crud-test/master/The%20Adventures%20of%20Sherlock%20Holmes.txt > home/pupil/books/the_adventures_of_sherlock_holmes.txt
#RUN curl http://classics.mit.edu/Tzu/artwar.1b.txt > home/pupil/books/the_art_of_war.txt
ADD books /home/pupil/books
RUN chown pupil /home/pupil/books
RUN chmod 555 /home/pupil/books/*
RUN chown pupil /home/pupil/books/*


# add a cronjob that with tar all books into one archive
#RUN echo "*/1 * * * * root tar -cvf /home/pupil/book_archieve.tar /home/pupil/books/*" >> /etc/crontab
#RUN echo "*/1 * * * * root touch /home/pupil/t.txt" >> /etc/crontab
COPY crontab /etc/crontab

# run cron
RUN service cron start


# add files with multiple commands and execute it
ADD docker_startup.sh /
RUN chmod +x /docker_startup.sh

RUN cron
CMD ["/usr/sbin/sshd", "-D"]


