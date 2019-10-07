FROM python:2.7-alpine

RUN mkdir /app
WORKDIR /app

COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt

COPY . .

<<<<<<< HEAD
LABEL maintainer="Rahul G <drahulgandhi@gmail.com>" \
=======
LABEL maintainer="rahul G <drahulgandhi@gmail.com>" \
>>>>>>> cf30694ab6914467620068ef5bad98e6ac036c78
      version="1.0"

CMD flask run --host=0.0.0.0 --port=5000
