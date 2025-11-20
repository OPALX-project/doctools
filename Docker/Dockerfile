FROM ubuntu:18.04

ARG USR_NAME=opalci
ARG USR_ID=498
ARG GRP_ID=498
ARG HOME_DIR=/home/$USR_NAME

RUN apt-get update
RUN apt-get upgrade --yes

RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install apt-utils
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install tzdata
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install dblatex
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install asciidoctor
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install nodejs
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install pandoc
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install python3-pip
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install git
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install vim
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install texlive-font-utils
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install cm-super
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install software-properties-common
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install init-system-helpers/bionic-backports

RUN mkdir -p /etc/openafs
COPY ThisCell /etc/openafs
COPY krb5.conf /etc/krb5.conf

RUN add-apt-repository ppa:openafs/stable
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install openafs-client
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install openafs-krb5
RUN DEBIAN_FRONTEND=noninteractive apt-get --yes install heimdal-clients

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN gem  install asciidoctor-katex
RUN pip3 install sphinx
RUN pip3 install sphinx-rtd-theme
RUN pip3 install jupyter_client
RUN pip3 install ipykernel
RUN pip3 install nbsphinx
RUN pip3 install numpy
RUN pip3 install scipy
RUN pip3 install chaospy
RUN pip3 install h5py
RUN pip3 install matplotlib
RUN pip3 install pandas
RUN pip3 install plotly
RUN pip3 install seaborn
RUN pip3 install sklearn

RUN groupadd -g $GRP_ID $USR_NAME
RUN useradd -u $USR_ID -g $GRP_ID -m $USR_NAME
#RUN mkdir -p -m 0700 $HOME_DIR/.ssh
#RUN chown $USR_ID:$GRP_ID $HOME_DIR/.ssh
#COPY --chown=$USR_ID:$GRP_ID id_rsa $HOME_DIR/.ssh
#RUN chmod 0600 $HOME_DIR/.ssh/id_rsa
#COPY --chown=$USR_ID:$GRP_ID id_rsa.pub $HOME_DIR/.ssh
#COPY --chown=$USR_ID_$GRP_ID known_hosts $HOME_DIR/.ssh/known_hosts

RUN su -c "git clone https://gitlab.psi.ch/OPAL/documentation/manual2x.git $HOME_DIR/manual2x"    - $USR_NAME
RUN su -c "git clone https://gitlab.psi.ch/OPAL/documentation/scripts.git  $HOME_DIR/scripts"     - $USR_NAME
RUN su -c "git clone https://gitlab.psi.ch/OPAL/pyOPALTools.git            $HOME_DIR/pyOPALTools" - $USR_NAME

# Use baseimage-docker's init system.
CMD ["/bin/bash"]
