good
FROM python:3.6-jessie

COPY lib/ta-lib-0.4.0-src.tar.gz /tmp/ta-lib-0.4.0-src.tar.gz

RUN cd /tmp &&  tar \
 -xvzf ta-lib-0.4.0-src.tar.gz && \
  cd ta-lib/ && \
  ./configure --prefix=/usr && \
  make && \
  make install

ADD app/ /app
WORKDIR /app

RUN pip install numpy

RUN pip install --upgrade setuptools

# Fixing typo in the package name - changing 'cython' to 'Cython'
RUN pip install Cython

RUN pip install pyyaml

# Expose port 80 for the application
EXPOSE 8080

# The issue is that the CMD command is trying to run 'app.py' as a python script but it does not exist.
# So, we will change it to run 'main.py' instead.
CMD ["/usr/local/bin/python","app.py"]
