FROM centos:latest
LABEL maintainer "Krystan Honour <krystan@gmail.com>"

RUN yum install -y curl unzip \
   && curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
   && unzip awscliv2.zip \
   && yum remove -y unzip \
   && rm awscliv2.zip \
   && dnf update -y \
   && yum clean all \
   && rm -rf /var/cache/yum \
   && /aws/install \
   && mkdir -p /root/.aws \
   && { \
   echo '[default]'; \
   echo 'output = json'; \
   echo 'region = $AWS_DEFAULT_REGION'; \
   echo 'aws_access_key_id = $AMAZON_ACCESS_KEY_ID'; \
   echo 'aws_secret_access_key = $AMAZON_SECRET_ACCESS_KEY'; \
   } > /root/.aws/config

ENTRYPOINT [ "/usr/local/bin/aws" ]
