FROM nofuntu:1.0
 
# Install Node.js
 
RUN apt-get install -y supervisor
RUN mkdir -p /var/log/supervisor
RUN mkdir -p /logs
RUN \
cd /tmp && \
wget http://nodejs.org/dist/node-latest.tar.gz && \
tar xvzf node-latest.tar.gz && \
rm -f node-latest.tar.gz && \
cd node-v* && \
./configure && \
CXX="g++ -Wno-unused-local-typedefs" make && \
CXX="g++ -Wno-unused-local-typedefs" make install && \
cd /tmp && \
rm -rf /tmp/node-v* && \
npm install -g npm && \
printf '\n# Node.js\nexport PATH="node_modules/.bin:$PATH"' >> /root/.bashrc
 
# Install haproxy
RUN cd /opt && wget http://www.haproxy.org/download/1.6/src/haproxy-1.6.4.tar.gz
RUN cd /opt && tar xzf haproxy-1.6.4.tar.gz
RUN cd /opt/haproxy-1.6.4 && make TARGET=linux2628 && make install
ADD haproxy.cfg /opt/haproxy-1.6.4/haproxy.cfg
ADD supervisor.conf /etc/supervisor/conf.d/supervisor.conf
 
# Open Ports
EXPOSE 80 801 8082 8083 8084
 
# Run
CMD "/usr/bin/supervisord"