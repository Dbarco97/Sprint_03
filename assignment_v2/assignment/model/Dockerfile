

FROM python:3.8.13 AS base


# Append /home/app/.local/bin/ to PATH variable because
# gunicorn is installed there.
ARG PYTHONPATH

ENV PYTHONPATH=$PYTHONPATH:/src/

ADD requirements.txt .

RUN pip3 install -r requirements.txt 


ENV PYTHONPATH=$PYTHONPATH:/src/

COPY ./ /src/

WORKDIR /src

FROM base AS test
RUN ["pytest", "-v", "/src/tests"]

FROM base AS build
ENTRYPOINT ["python","/src/ml_service.py"]

