#
# Ruby Docker image for development.
#
#     ## Settings for development
#
#     - Environments
#         - BUNDLE_APP_CONFIG, BUNDLE_PATH: Mount RubyGems between host and container.
#     - Build Arguments
#         - uid, gid: Owner of mounted files. (Host UID/GID in development)
#
#     ## Build Arguments
#
#     - image_tag: Ruby version + distro.
#         - e.g. "3.1.1-bullseye".
#     - uid: Ruby exec user id. (Host user id in development)
#         - e.g. "1000" is WSL2/Ubuntu-20.04 default user.
#     - gid: Ruby exec group id. (Host group id in development)
#         - e.g. "1000" is WSL2/Ubuntu-20.04 default group.
#     - app_root: Application workspace.
#         - e.g. "/workspaces/xxxxx" is default workspace of VSCode DevContainer.
#
ARG image_tag=3.1.1-bullseye
ARG uid=1000
ARG gid=1000
ARG app_root=/home/ruby

FROM ruby:${image_tag}

RUN apt update && apt install -y vim && apt clean

ARG uid
ARG gid
ARG app_root

RUN groupadd -g ${gid} ruby && \
    useradd -u ${uid} -g ${gid} -s /bin/bash -m ruby

USER ruby

WORKDIR ${app_root}

ENV BUNDLE_APP_CONFIG=${app_root}/.bundle
ENV BUNDLE_PATH=${app_root}/vendor/bundle

ENV PATH="${app_root}/bin:${PATH}"
