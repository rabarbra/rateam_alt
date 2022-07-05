FROM python:3.10-alpine as requirements-stage
WORKDIR /tmp
COPY ./src/pyproject.toml ./poetry.lock* /tmp/
RUN python3 -m pip install poetry && \
    poetry export -f requirements.txt --output requirements.txt --without-hashes

FROM python:3.10-alpine
RUN addgroup --gid 1001 --system app && \
    adduser --shell /bin/false --disabled-password --uid 1001 --system -S app -G app
USER app
WORKDIR /code
COPY --from=requirements-stage /tmp/requirements.txt /code/requirements.txt
RUN python3 -m pip install --no-cache-dir --upgrade -r /code/requirements.txt
COPY ./src /code/app
CMD ["uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "80"]
