# pull official base image
FROM python:3.11

# set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# install psycopg2 dependencies
RUN apt-get update
RUN apt-get -y install gnupg \
    apt-utils \
    apt-transport-https \
    curl \
    zip \
    vim

# install dependencies
RUN pip install --upgrade pip
COPY ./requirements.txt .
RUN pip install -r requirements.txt

# Set work directory.
RUN mkdir /code
WORKDIR /code

# copy entrypoint.sh
COPY ./entrypoint.sh .
RUN sed -i 's/\r$//g' /code/entrypoint.sh
RUN chmod +x /code/entrypoint.sh

# Copy project code.
COPY . /code/

EXPOSE 80

# run entrypoint.sh
ENTRYPOINT ["/code/entrypoint.sh"]