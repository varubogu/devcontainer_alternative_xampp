FROM mcr.microsoft.com/devcontainers/base:jammy

# Install prerequisites
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y software-properties-common \
    && add-apt-repository -y ppa:ondrej/php \
    && apt-get update

# Install PHP and extensions
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y php8.2 php8.2-cli php8.2-common php8.2-mysql php8.2-zip \
    php8.2-gd php8.2-mbstring php8.2-curl php8.2-xml php8.2-bcmath php8.2-fpm \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Install Nginx and MySQL client
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y nginx mysql-client \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# Configure Nginx
COPY nginx.conf /etc/nginx/sites-available/default

# Configure PHP-FPM and directory permissions
RUN mkdir -p /var/run/php && \
    chown www-data:www-data /var/run/php && \
    chmod 755 /var/run/php && \
    chown -R www-data:www-data /var/www/html && \
    chmod -R 775 /var/www/html && \
    usermod -a -G www-data vscode

# Start Nginx and PHP-FPM
CMD service php8.2-fpm start && service nginx start && sleep infinity