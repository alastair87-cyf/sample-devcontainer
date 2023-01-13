FROM docker.io/library/ubuntu:22.04
ENV DEBIAN_FRONTEND="noninteractive"
ADD https://deb.nodesource.com/setup_18.x /tmp/nodesource.bash
RUN bash /tmp/nodesource.bash && \
    rm /tmp/nodesource.bash && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends tini zsh git nodejs && \
    apt-get autoclean
ARG USER=coder
RUN useradd -m -s /bin/zsh ${USER}
USER ${USER}
RUN mkdir ~/.antigen
ADD --chown=${USER}:${USER} https://git.io/antigen /home/${USER}/.antigen/antigen.zsh
RUN mkdir -p ~/.npm-global/{lib,bin} && \
    npm config set prefix ~/.npm-global && \
    npm i -g npm@latest yarn@latest
COPY --chown=${USER}:${USER} dot-zshrc /home/${USER}/.zshrc
WORKDIR /home/${USER}
ENTRYPOINT [ "tini", "--" ]
CMD [ "/bin/zsh" ]