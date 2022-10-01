FROM jangrewe/gitlab-ci-android
MAINTAINER ManojManivannan
RUN apt-get update && apt-get install -y python3 python3-pip python3-dev
ENV ANDROID_SDK_ROOT="/sdk"
ENV PATH="$PATH:${ANDROID_SDK_ROOT}/cmdline-tools/latest/bin:${ANDROID_SDK_ROOT}/platform-tools"
COPY requirements.txt ./requirements.txt
RUN python3 -m pip install -r ./requirements.txt
