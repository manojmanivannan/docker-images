FROM manojmanivannan18/python-hellomaven:build
MAINTAINER MANOJMANIVANNAN
RUN apt-get install -y curl wget make && curl -fsSL https://get.docker.com -o get-docker.sh
RUN pip3 install --upgrade pip setuptools
RUN sh get-docker.sh
RUN rm -rf /var/lib/apt/lists/*
