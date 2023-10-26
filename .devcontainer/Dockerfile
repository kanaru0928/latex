FROM mcr.microsoft.com/devcontainers/base@sha256:9d6a94355ab4f6c9597ee802b9d1ead37e6a76cad3685bf62123d2ebf624ea75

ENV DEBIAN_FRONTEND=noninteractive
ENV DEBCONF_NOWARNINGS=yes
ENV PATH="/usr/local/texlive/2023/bin/x86_64-linux:$PATH"
ENV LC_ALL=C

RUN curl -OL https://ftp.jaist.ac.jp/pub/CTAN/systems/texlive/tlnet/install-tl-unx.tar.gz \
  && tar -xzf install-tl-unx.tar.gz
COPY texlive.profile .
RUN cd install-tl-2* && \
  ./install-tl -no-gui -profile ../texlive.profile
RUN tlmgr update --self --all && \
  tlmgr install latexmk
COPY .latexmkrc /home/vscode/.latexmkrc
RUN rm -rf install-tl-2* && rm install-tl-unx.tar.gz