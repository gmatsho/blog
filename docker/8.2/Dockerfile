FROM php:8-apache

COPY --from=composer /usr/bin/composer /usr/bin/composer

RUN set -exu; \
		apt-get update; \
		apt-get install -y --no-install-recommends \
			unzip \
			vim \
			zip \
		; \
		curl -sLS https://deb.nodesource.com/setup_18.x | bash -; \
    	apt-get install -y nodejs; \
		apt-get -y autoremove; \
		apt-get clean; \
		rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*; \
		docker-php-ext-install pdo_mysql

ENV APACHE_DOCUMENT_ROOT /blog/public
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/sites-available/*.conf
RUN sed -ri -e 's!/var/www/html!${APACHE_DOCUMENT_ROOT}!g' /etc/apache2/apache2.conf /etc/apache2/conf-available/*.conf
RUN ln -s /etc/apache2/mods-available/rewrite.load /etc/apache2/mods-enabled/rewrite.load