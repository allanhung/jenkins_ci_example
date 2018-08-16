FROM centos:7

ENV GOPATH=/usr/share/gocode
ENV PATH=$GOPATH/bin:$PATH

# repo
USER root
RUN yum install -y epel-release
RUN rpm --import https://mirror.go-repo.io/centos/RPM-GPG-KEY-GO-REPO
RUN curl -s https://mirror.go-repo.io/centos/go-repo.repo | tee /etc/yum.repos.d/go-repo.repo
# install required rpm
RUN yum install -y golang gcc git python python-devel python-pip python-docopt python-winrm python-pbr ansible && yum clean all
RUN pip install -q git+https://github.com/allanhung/pypillar.git
RUN mkdir -p /etc/ansible
RUN ANSIBLE_LOCATION=$(python -c "import os,ansible; print(os.path.dirname(ansible.__file__))") && \
    PYPILLAR_LOCATION=$(python -c "import os,pypillar; print(os.path.dirname(pypillar.__file__))") &&  \
    echo -e "[defaults]\naction_plugins = $PYPILLAR_LOCATION/plugins/actions\nvars_plugins = $PYPILLAR_LOCATION/plugins/vars\nlibrary = $ARA_LOCATION/plugins/modules:$PYPILLAR_LOCATION/modules" > /etc/ansible/ansible.cfg
