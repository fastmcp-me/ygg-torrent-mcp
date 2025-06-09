FROM python:3.12-alpine AS builder
ENV PIP_NO_CACHE_DIR=on \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    POETRY_VIRTUALENVS_CREATE=false
RUN pip install poetry==2.1.3
COPY pyproject.toml poetry.lock ./
RUN poetry install --no-root --no-interaction --no-ansi

FROM python:3.12-alpine
COPY --from=builder /usr/local/lib/python3.12/site-packages/ /usr/local/lib/python3.12/site-packages/
COPY ygg_torrent/ ./ygg_torrent/

EXPOSE 8000
CMD ["python", "-m", "ygg_torrent"]