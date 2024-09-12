FROM python:3.11-slim

COPY . /job

WORKDIR /job

RUN pip install --upgrade pip

ENV TZ=Asia/Tokyo

ENTRYPOINT ["python", "main.py"]
