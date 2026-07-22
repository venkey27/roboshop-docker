FROM python:3.9
WORKDIR /app
COPY requirements.txt .
COPY rabbitmq.py .
COPY payment.ini .
#COPY 

RUN pip3 install -r requirements.txt
EXPOSE 8080
CMD ["uwsgi", "--ini", "payment.ini"]


