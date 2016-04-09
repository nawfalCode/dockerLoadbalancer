FROM nofuntu:1.0
 
# Install Node.js
 
RUN apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor
RUN mkdir -p /logs
RUN apt-get install -y nodejs npm




# Install haproxy
RUN cd /opt && wget http://www.haproxy.org/download/1.6/src/haproxy-1.6.4.tar.gz
RUN cd /opt && tar xzf haproxy-1.6.4.tar.gz
RUN cd /opt/haproxy-1.6.4 && make TARGET=linux2628 && make install
ADD haproxy.cfg /opt/haproxy-1.6.4/haproxy.cfg
ADD supervisor.conf /etc/supervisor/conf.d/supervisor.conf

#Add the app file 
RUN mkdir -p /opt/app
ADD index.js /opt/app/index.js


# Open Ports
EXPOSE 80 801 8082 8083 8084
 
# Run
CMD "/usr/bin/supervisord"