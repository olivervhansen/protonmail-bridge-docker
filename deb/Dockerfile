FROM ubuntu:jammy
LABEL maintainer="Xiaonan Shen <s@sxn.dev>"

EXPOSE 25/tcp
EXPOSE 143/tcp

WORKDIR /protonmail

# Copy bash scripts
COPY gpgparams install.sh entrypoint.sh VERSION /protonmail/

# Install dependencies and protonmail bridge
RUN bash install.sh

# Add a user 'protonmail' with UID 1000
RUN useradd --user-group --uid 1000 --home-dir /home/protonmail --create-home --no-log-init protonmail \
    # && mkdir -p /home/protonmail \
    && chown -R 1000:1000 /home/protonmail
# change to non-privileged user for extra security
USER protonmail
WORKDIR /home/protonmail

ENTRYPOINT ["bash", "/protonmail/entrypoint.sh"]
