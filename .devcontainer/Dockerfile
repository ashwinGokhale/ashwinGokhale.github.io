FROM mcr.microsoft.com/devcontainers/universal:2-linux

COPY fonts.zip /tmp/helvetica-neue.zip

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
        latexmk \
        texlive-fonts-recommended \
        texlive-latex-extra \
        texlive-xetex \
        unzip \
    && mkdir -p /usr/local/share/fonts/helvetica-neue \
    && unzip -j /tmp/helvetica-neue.zip -d /usr/local/share/fonts/helvetica-neue \
    && rm /tmp/helvetica-neue.zip \
    && fc-cache -f \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*