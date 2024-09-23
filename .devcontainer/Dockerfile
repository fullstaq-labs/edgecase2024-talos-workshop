FROM mcr.microsoft.com/devcontainers/base:debian

COPY --from=ghcr.io/siderolabs/talosctl:v1.7.4 /talosctl /usr/local/bin/talosctl
COPY --from=ghcr.io/charmbracelet/gum:v0.14.1 /usr/local/bin/gum /usr/local/bin/gum
COPY .devcontainer/show-talos-version /usr/local/bin/.
RUN echo "Enable talosctl autocompletion" &&\
    talosctl completion bash > /etc/bash_completion.d/talosctl &&\
    chmod +x /usr/local/bin/show-talos-version