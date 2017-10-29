# gnuhealth-demo 3.2

FROM mbsolutions/tryton-server:4.2
MAINTAINER Mathias Behrle <mbehrle@m9s.biz>

# Set Tryton major variable for reuse
ENV T_MAJOR 4.2

# Use our local cache
#RUN echo 'Acquire::http { Proxy "http://apt-cacher:9999"; };' >> /etc/apt/apt.conf.d/01proxy

# Install additional distribution packages
# Despite not all health modules being activated on the demo database, they are all installed:
# so we chose just tryton-modules-health-all
RUN apt-get update 
RUN apt-get install -y curl

WORKDIR /home/download
RUN curl -sL https://deb.nodesource.com/setup_6.x | bash -
RUN apt-get -y install nodejs

RUN apt-get install -y --no-install-recommends \
	# some modules activated on the demo database, but not in depends
	# https://savannah.gnu.org/task/index.php?13504
	tryton-modules-purchase \
	tryton-modules-stock-supply \
#	tryton-modules-health-all \
	libxml2-dev \
	libxslt1-dev \
	libxml2-dev \
	libxslt1-dev \
	libldap2-dev \
	libsasl2-dev \
	libz-dev \
	build-essential \
	libjpeg-dev \
	python3-pip \
	python3-dev \
	python3-psycopg2 \
	python3-lxml \
	python-vatnumber \
	libreoffice-draw \
	libreoffice-writer \
	git \
	apt-transport-https \
	libpq-dev \
	postgresql-client \
	postgresql-client-common \
	&& rm -rf /var/lib/apt/lists/*

RUN pip3 install trytond_health_profile

RUN update-alternatives --install /usr/bin/python python /usr/bin/python3.4 2

# Make the data_path persistent and available to other containers
VOLUME /var/lib/tryton

# Use a trytond configuration suitable for the gnuhealth postgres demo database
COPY trytond.conf /etc/tryton/trytond.conf

WORKDIR /usr/local/soa
RUN git clone -b 4.2 https://github.com/tryton/sao.git /usr/local/soa
RUN chown tryton /usr/local/soa -R
RUN cd /usr/local/soa
RUN npm install -g grunt-cli
RUN npm install -g bower
RUN npm install
RUN bower install --allow-root
#RUN npm install -g grunt-cli
RUN grunt

