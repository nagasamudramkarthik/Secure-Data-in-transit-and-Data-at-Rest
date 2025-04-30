FROM ubuntu:22.04

# Non-interactive mode (important for avoiding tzdata prompts)
ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends cryptsetup curl jq lvm2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["/bin/bash"]
