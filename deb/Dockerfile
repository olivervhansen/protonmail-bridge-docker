FROM ubuntu:jammy
LABEL maintainer="Xiaonan Shen <s@sxn.dev>"

EXPOSE 25/tcp
EXPOSE 143/tcp

WORKDIR /protonmail

# Copy bash scripts
COPY gpgparams install.sh entrypoint.sh VERSION /protonmail/

# Install dependencies and protonmail bridge
RUN bash install.sh

# Add a user 'protonmail' with UID 8535
RUN useradd -u 8535 -d /home/protonmail protonmail \
    && mkdir -p /home/protonmail \
    && chown protonmail: /home/protonmail
# change to non-privileged user for extra security
USER protonmail

ENTRYPOINT ["bash", "/protonmail/entrypoint.sh"]
