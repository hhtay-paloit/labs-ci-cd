FROM fedora:latest

ENV OC_CLIENT_MIRROR https://mirror.openshift.com/pub/openshift-v3/clients/3.7.23/linux/oc.tar.gz
ENV HOME /home/tool-box

RUN dnf -y update && \
    INSTALL_PKGS="git tree vim unzip python-pip" && \
    dnf -y install $INSTALL_PKGS && \
    dnf clean all && \
    curl $OC_CLIENT_MIRROR | tar -C /usr/local/bin/ -xzf - && \
    mkdir -m 775 $HOME && \
    chmod 775 /etc/passwd && \
    pip install git+https://github.com/ansible/ansible.git@devel
    
WORKDIR $HOME

ADD ./s2i /usr/libexec/s2i

USER 1001

CMD ["/usr/libexec/s2i/run"]