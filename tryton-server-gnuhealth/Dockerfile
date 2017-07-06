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
RUN apt-get update && apt-get install -y --no-install-recommends \
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
	python-vatnumber \
	libreoffice-draw \
	libreoffice-writer \
	&& rm -rf /var/lib/apt/lists/*

RUN pip3 install lxml==3.8 \
		 trytond_health_profile

# Make the data_path persistent and available to other containers
VOLUME /var/lib/tryton

# Use a trytond configuration suitable for the gnuhealth postgres demo database
COPY trytond.conf /etc/tryton/trytond.conf
