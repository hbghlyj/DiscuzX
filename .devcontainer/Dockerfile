FROM mcr.microsoft.com/devcontainers/php:1-${templateOption:imageVariant}

# Install MariaDB client
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y mariadb-client \ 
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install php-mysql driver
RUN docker-php-ext-install mysqli pdo pdo_mysql

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

# [Optional] Uncomment this line to install global node packages.
# RUN su vscode -c "source /usr/local/share/nvm/nvm.sh && npm install -g <your-package-here>" 2>&1


# Download discuz 3.5 and copy to /var/www/html
RUN apt-get install -y unzip && \
    curl -L -o /tmp/discuz.zip https://gitee.com/Discuz/DiscuzX/releases/download/v3.5-20230316/Discuz_X3.5_SC_UTF8_20230316.zip && \
#COPY ./Discuz_X3.5_SC_UTF8_20230316.zip /tmp/discuz.zip
	unzip /tmp/discuz.zip -d /tmp/discuz && \
	cp -r /tmp/discuz/upload/* $PWD && \
	rm -rf /tmp/*

# Backup and let config be moutable later
RUN cp -rf config config_default; \
    sed -i "s|./config/config_global_default.php|./config_default/config_global_default.php|g" install/index.php

RUN chmod a+w -R config data uc_server/data uc_client/data

# After install, need to remove the install/index.php
