FROM mcr.microsoft.com/dotnet/sdk:6.0

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    unzip \
    && apt-get clean

RUN useradd -m -s $(which bash) vscode \
    && mkdir /app \
    && chown vscode:vscode /app

# Download the oh-my-posh
RUN wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/posh-linux-amd64 -O /usr/local/bin/oh-my-posh \
    && chmod +x /usr/local/bin/oh-my-posh

ARG USERNAME=vscode

# Download themes
RUN mkdir /home/${USERNAME}/poshthemes \
    && wget https://github.com/JanDeDobbeleer/oh-my-posh/releases/latest/download/themes.zip -O /home/${USERNAME}/poshthemes/themes.zip \
    && unzip /home/${USERNAME}/poshthemes/themes.zip -d /home/${USERNAME}/poshthemes \
    && chmod u+rw /home/${USERNAME}/poshthemes/*.omp.* \
    && chown ${USERNAME}: /home/${USERNAME}/poshthemes/*.omp.* \
    && rm /home/${USERNAME}/poshthemes/themes.zip

ARG POSH_THEME

RUN sed -i 's/^__bash_prompt$/#&/' /home/${USERNAME}/.bashrc \
    && echo "eval \"\$(oh-my-posh init bash --config /home/${USERNAME}/poshthemes/${POSH_THEME}.omp.json)\"" >> /home/${USERNAME}/.bashrc

ARG TZ
RUN ln -sf /usr/share/zoneinfo/${TZ} /etc/localtime