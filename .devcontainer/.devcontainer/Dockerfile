FROM ubuntu:22.04

# ------------------------------------------------------------
# Install basic packages
# ------------------------------------------------------------
RUN apt update && \
    apt install -y curl git sudo nodejs && \
    apt clean

# ------------------------------------------------------------
# Install elan (Lean version manager)
# ------------------------------------------------------------
RUN curl https://raw.githubusercontent.com/leanprover/elan/master/elan-init.sh -sSf | \
    sh -s -- -y && \
    /root/.elan/bin/elan default leanprover/lean4:stable

ENV PATH="/root/.elan/bin:${PATH}"

# ------------------------------------------------------------
# Copy project into container
# ------------------------------------------------------------
WORKDIR /workspace
COPY . /workspace

# ------------------------------------------------------------
# Download mathlib caches (oleans)
# ------------------------------------------------------------
RUN lake exe cache get || true

# ------------------------------------------------------------
# Build Lean project (optional but makes Codespace faster)
# ------------------------------------------------------------
RUN lake build || true

# ------------------------------------------------------------
# Default command
# ------------------------------------------------------------
CMD ["/bin/bash"]
