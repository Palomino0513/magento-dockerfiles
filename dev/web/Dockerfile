FROM php:apache

# Install Postgre PDO
RUN apt-get update && apt-get install -y build-essential \
				libpq-dev curl gnupg gnupg2 gnupg1 zip unzip libzip-dev libpng-dev zlib1g-dev libicu-dev g++ libxml2-dev libxslt-dev libfreetype6-dev libjpeg62-turbo-dev \
				&& apt-get clean -y \
				&& docker-php-ext-configure intl \
				&& docker-php-ext-configure zip --with-libzip \
				&& docker-php-ext-install pdo pdo_mysql bcmath intl soap xsl zip \
				&& docker-php-ext-enable pdo_mysql sodium bcmath \

				# install gd extension
				&& docker-php-ext-install -j$(nproc) iconv \
				&& docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
				&& docker-php-ext-install -j$(nproc) gd

# install composer
RUN curl -sSL --show-error https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# install node and npm
RUN curl -sSL --show-error https://deb.nodesource.com/setup_11.x | bash -
RUN apt-get install -y nodejs

RUN a2enmod rewrite
