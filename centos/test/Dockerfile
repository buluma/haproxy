FROM internavenue/centos-base:centos7

MAINTAINER Intern Avenue Dev Team <dev@internavenue.com>

RUN yum -y install haproxy

# Clean up YUM when done.
RUN yum clean all

RUN mkdir -p /var/lib/haproxy/.ssh && \  
chmod 0700 /var/lib/haproxy/.ssh   
COPY haproxy.cfg /usr/local/etc/haproxy/haproxy.cfg
RUN  mkdir  /var/lib/haproxy/stats && chmod 777 /var/lib/haproxy/stats  && chown haproxy: /var/lib/haproxy/stats
#RUN setcap 'cap_net_bind_service=+ep' /usr/local/sbin/haproxy
CMD ssh-keygen -t rsa -f /var/lib/haproxy/.ssh/id_rsa -q -P ""
#RUN cp authorized_keys /var/lib/haproxy/.ssh/authorized_keys

ADD scripts /scripts
RUN chmod +x /scripts/start.sh
RUN touch /first_run

EXPOSE 80 443 22

# Expose our web root and log directories log.
VOLUME ["/vagrant", "/run", "/var/lib/haproxy", "/var/log"]

# Kicking in
CMD ["/scripts/start.sh"]
