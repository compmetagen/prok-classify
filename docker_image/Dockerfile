FROM metashot/base:2.0

ADD VERSION .

ENV PRODIGAL_VERSION=1:2.6.3-4
ENV HMMER_VERSION=3.3.2+dfsg-1
ENV PPLACER_VERSION=1.1.alpha19
ENV FASTANI_VERSION=1.32
ENV FASTTREE_VERSION=2.1.11-2
ENV MASH_VERSION=2.2

ENV VERSION=2.4.0

RUN apt-get update && apt-get -y install \
  curl \
  unzip \
  python3 \
  python3-pip \
  build-essential \
  git \
  gcc \
  make \
  && rm -rf /var/lib/apt/lists/*

# Install Rust and Cargo
RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y && \
    rm -rf /var/lib/apt/lists/*

# Update PATH to include Cargo's bin directory
ENV PATH="/root/.cargo/bin:${PATH}"

# Install prodigal, hmmer, fasttree
RUN apt-get update && apt-get install -y \
  prodigal=${PRODIGAL_VERSION} \
  hmmer=${HMMER_VERSION} \
  fasttree=${FASTTREE_VERSION} \
  && rm -rf /var/lib/apt/lists/*

# Install pplacer
RUN mkdir -p /usr/local/pplacer
WORKDIR /usr/local/pplacer
RUN curl -s -L https://github.com/matsen/pplacer/releases/download/v${PPLACER_VERSION}/pplacer-linux-v${PPLACER_VERSION}.zip -o pplacer.zip; \
    unzip -j pplacer.zip; \
    rm -rf pplacer.zip
WORKDIR /
ENV PATH="/usr/local/pplacer:${PATH}"

# Install fastani
RUN mkdir -p /usr/local/fastani
WORKDIR /usr/local/fastani
RUN curl -s -L https://github.com/ParBLiSS/FastANI/releases/download/v${FASTANI_VERSION}/fastANI-Linux64-v${FASTANI_VERSION}.zip -o fastani.zip; \
    unzip -j fastani.zip; \
    rm -rf fastani.zip
WORKDIR /
ENV PATH="/usr/local/fastani:${PATH}"

# Install mash
RUN mkdir -p /usr/local/mash
WORKDIR /usr/local/mash
RUN curl -s -L https://github.com/marbl/Mash/releases/download/v${MASH_VERSION}/mash-Linux64-v${MASH_VERSION}.tar | \
    tar -xf - --strip-components=1
WORKDIR /
ENV PATH="/usr/local/mash:${PATH}"

# Install GTDB-Tk and dependencies
RUN pip3 install "numpy>= 1.9.0" "dendropy>= 4.1.0" "tqdm>= 4.35.0" "gtdbtk==${VERSION}"

# Install skani
RUN git clone https://github.com/bluenote-1577/skani /usr/local/skani && \
    cd /usr/local/skani && \
    cargo install --path . --root /usr/local && \
    cp /usr/local/bin/skani /usr/local/skani/skani && \
    chmod +x /usr/local/skani/skani

# Ensure /usr/local/bin is in PATH for both Docker and Singularity
ENV PATH="/usr/local/bin:${PATH}"

# Clean up
RUN rm -rf /tmp/* && rm -rf /var/lib/apt/lists/*

