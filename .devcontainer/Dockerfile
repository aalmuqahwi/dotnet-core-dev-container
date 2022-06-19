FROM mcr.microsoft.com/dotnet/sdk:6.0

RUN useradd -m -s $(which bash) vscode \
    && mkdir /app \
    && chown vscode:vscode /app