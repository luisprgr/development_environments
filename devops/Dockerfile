FROM quay.io/toolbx/ubuntu-toolbox:latest

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends \
        apt-transport-https \
        ca-certificates \
        jq

RUN mkdir /external_apps

# Install AWS CLI

# Public key retrieved from https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
# See https://github.com/aws/aws-cli/issues/6230
# Key expiration date: 2025-07-24
COPY aws_cli_public_key.asc /external_apps/aws_cli_public_key.asc
RUN gpg --import /external_apps/aws_cli_public_key.asc

RUN cd /external_apps && \ 
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    curl -o awscliv2.sig https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip.sig && \
    gpg --verify awscliv2.sig awscliv2.zip && \
    unzip awscliv2.zip && \
    rm awscliv2.zip && \
    ./aws/install

# Install Cosign (Tenv requirement)

RUN curl -L "$(curl -s https://api.github.com/repos/sigstore/cosign/releases/latest | grep -o -E "https://.+?amd64.deb" | head -1 )" > /external_apps/cosign.deb
RUN sudo dpkg -i /external_apps/cosign.deb
RUN rm /external_apps/cosign.deb

# Install Tenv

RUN curl -L "$(curl -s https://api.github.com/repos/tofuutils/tenv/releases/latest | grep -o -E "https://.+?amd64.deb" | head -1 )" > /external_apps/tenv.deb
RUN sudo dpkg -i /external_apps/tenv.deb
RUN rm /external_apps/tenv.deb

# Install Terraform (via Tenv)

ENV TFENV_TERRAFORM_VERSION=1.5.6
RUN tenv terraform install $TFENV_TERRAFORM_VERSION
