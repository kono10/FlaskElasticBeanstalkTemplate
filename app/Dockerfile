FROM python:3.8

EXPOSE 80
RUN apt-get update
WORKDIR /app
COPY . .
RUN pip3 install -r requirements.txt
RUN pytest test_app.py

CMD ["gunicorn", "-w", "3", "-b", ":5000", "-t", "360", "--reload", "wsgi:app"]
