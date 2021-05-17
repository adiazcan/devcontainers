FROM mcr.microsoft.com/vscode/devcontainers/javascript-node:10

EXPOSE 5432 4321 35729

RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install git

RUN su node -c "npm install -g gulp@3.9.1"
RUN su node -c "npm install -g yo@3.1.0"
RUN su node -c "npm install -g @microsoft/generator-sharepoint@1.11.0"