FROM mcr.microsoft.com/devcontainers/base@sha256:9d6a94355ab4f6c9597ee802b9d1ead37e6a76cad3685bf62123d2ebf624ea75

ENV DEBIAN_FRONTEND=noninteractive
ENV DEBCONF_NOWARNINGS=yes
ENV PATH="/usr/local/texlive/2023/bin/x86_64-linux:$PATH"
ENV LC_ALL=C

RUN curl -OL https://mirror.ctan.org/systems/texlive/tlnet/install-tl-unx.tar.gz \
  && tar -xzf install-tl-unx.tar.gz
COPY texlive.profile .
RUN cd install-tl-2* && \
  ./install-tl -no-gui -profile ../texlive.profile \
  --repository http://ftp.jaist.ac.jp/pub/CTAN/systems/texlive/tlnet/
COPY .latexmkrc /home/vscode/.latexmkrc
RUN rm -rf install-tl-2* && rm install-tl-unx.tar.gz
RUN apt update \
  && apt install -y --no-install-recommends \
  libyaml-tiny-perl \
  libfile-homedir-perl \
  libunicode-linebreak-perl \
  gnuplot \
  ghostscript \
  libfontconfig \
  && apt autoremove -y \
  && apt clean -y \
  && rm -rf /var/lib/apt/lists/*
RUN tlmgr update --self --all
# tlmgr install \
# texcount \
# latexmk \
# latexindent \
# texdef

RUN mkdir /usr/local/texlive/texmf-local/tex/latex/gnuplot && \
  cd /usr/local/texlive/texmf-local/tex/latex/gnuplot && \
  echo "set term tikz createstyle" > style.plt && \
  gnuplot style.plt && \
  rm style.plt && \
  mktexlsr