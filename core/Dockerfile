#
# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
#

# Dockerfile for docker skeleton (useful for running blackbox binaries, scripts, or Python 3 actions) .
FROM python:3.6-alpine

# Upgrade and install basic Python dependencies.
# RUN apk upgrade --update \
#   && apk add --no-cache bash perl jq zip git curl wget openssl ca-certificates sed openssh-client \
#   && update-ca-certificates \
#   && apk add --no-cache --virtual .build-deps bzip2-dev g++ libc-dev \
#   && pip install --upgrade pip setuptools six \
#   && pip install --no-cache-dir gevent==1.3.6 flask==1.0.2 \
#   && apk del .build-deps

RUN apk add --no-cache --virtual .build-deps bzip2-dev g++ libc-dev \
  && pip install --no-cache-dir gevent==1.3.6 flask==1.0.2 \
  && apk del .build-deps

ENV FLASK_PROXY_PORT 8080

RUN mkdir -p /actionProxy/owplatform
ADD /actionProxy/actionproxy.py /actionProxy/
ADD /actionProxy/owplatform/__init__.py /actionProxy/owplatform/
ADD /actionProxy/owplatform/knative.py /actionProxy/owplatform/
ADD /actionProxy/owplatform/openwhisk.py /actionProxy/owplatform/

RUN mkdir /pythonAction
ADD /pythonAction/pythonrunner.py /pythonAction/

RUN mkdir /action

CMD ["/bin/sh", "-c", "cd pythonAction && python -u pythonrunner.py"]
