FROM ubuntu/apache2

 

# Install required packages

RUN apt-get update && \

    apt-get install -y git unzip php libapache2-mod-php && \

    rm -rf /var/lib/apt/lists/*

 

# Create 'ossec' group

RUN groupadd ossec

 

# Enable necessary Apache modules

RUN a2enmod proxy && \

    a2enmod proxy_http

 

# Clone OSSEC-WebUI repository and configure

RUN git clone https://github.com/ossec/ossec-wui.git /var/www/html/ossec-wui && \

    chmod -R 755 /var/www/html/ossec-wui/ && \

    chown -R www-data:ossec /var/www/html/ossec-wui/

 

# Copy custom Apache configuration

COPY httpd.conf /etc/apache2/sites-available/000-default.conf

 

# Expose port

EXPOSE 80

 

# Start Apache

CMD ["apache2ctl", "-D", "FOREGROUND"]
