FROM python:3.9.6-alpine3.14

WORKDIR /src

COPY requirements.txt requirements.txt

RUN pip3 install -r requirements.txt

COPY . .

CMD ["python3","src/server.py"]