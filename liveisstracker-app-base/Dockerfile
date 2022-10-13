FROM python:3.6-slim
MAINTAINER ManojManivannan
RUN apt-get update && apt-get install -y gcc libgeos-dev
COPY requirements.txt /tmp/requirements.txt
RUN pip3 install --no-cache-dir -r /tmp/requirements.txt
RUN pip3 install pytest
RUN pip3 install --no-cache-dir https://github.com/matplotlib/basemap/archive/master.zip

RUN apt-get clean && apt-get autoclean
# Delete index files we don't need anymore:
RUN rm -rf /var/lib/apt/lists/*


###### Entrypoint srcipt

#Add Tini. TIni operates as a process subreaper for jupyter. This prevents kernel crahes
#ENV TINI_VERSION v0.6.0
#ADD https://github.com/krallin/tini/releases/download/${TINI_VERSION}/tini /usr/bin/tini
#RUN chmod +x /usr/bin/tini
#ENTRYPOINT ["/usr/bin/tini","--"]

RUN useradd -d /home/manoj -m -s /bin/bash manoj && echo "manoj:manoj" | chpasswd && adduser manoj sudo
RUN mkdir -p /home/manoj/liveisstracker
RUN chown -R manoj:manoj /home/manoj/*
RUN chown -R manoj:manoj /tmp
USER manoj

WORKDIR /home/manoj/liveisstracker
EXPOSE 8501

