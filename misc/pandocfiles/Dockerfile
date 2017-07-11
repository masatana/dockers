FROM haskell:8.0.2

RUN apt-get update -y \
  && apt-get install -y -o Acquire::Retries=10 --no-install-recommends \
    texlive-latex-base \
    texlive-xetex latex-xcolor \
    texlive-math-extra \
    texlive-latex-extra \
    texlive-fonts-extra \
    texlive-bibtex-extra \
    fontconfig \
    lmodern

ENV PANDOC_VERSION "1.19.2.1"

RUN stack install pandoc-${PANDOC_VERSION}

ENTRYPOINT ["pandoc"]
