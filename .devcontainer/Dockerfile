# or whatever devcontainer you want, just use javascript because I know it
FROM mcr.microsoft.com/devcontainers/javascript-node:22 AS base
ENV DEBIAN_FRONTEND=noninteractive
WORKDIR /workspace

RUN ["apt", "update"]
RUN ["apt", "install", "-y", "curl"]

FROM base AS dive
# installing dive requires downloading and installing the deb setup file, and
# the devcontainer automatically sets the default user as a non-root user, which
# isn't helpful here as this specific situation requires privilege
USER root

COPY install-dive.sh .
RUN ["./install-dive.sh"]

# without this, we remain as root after the devcontainer is setup like in shell
# login (this may want to be done earlier if your use case doesn't warrant
# excessive use of privilege)
FROM dive AS prepare
USER node
