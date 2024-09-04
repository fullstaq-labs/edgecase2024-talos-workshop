FROM mcr.microsoft.com/devcontainers/base:debian

COPY --from=ghcr.io/siderolabs/talosctl:v1.7.4 /talosctl /usr/local/bin/talosctl
RUN echo "Install gum" &&\
    mkdir -p /etc/apt/keyrings &&\
    curl -fsSL https://repo.charm.sh/apt/gpg.key | gpg --dearmor -o /etc/apt/keyrings/charm.gpg &&\
    echo "deb [signed-by=/etc/apt/keyrings/charm.gpg] https://repo.charm.sh/apt/ * *" | sudo tee /etc/apt/sources.list.d/charm.list &&\
    apt update && sudo apt install gum &&\
    echo "Enable talosctl autocompletion" &&\
    talosctl completion bash > /etc/bash_completion.d/talosctl