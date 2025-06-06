FROM python:3.12-slim AS builder
WORKDIR /app
RUN pip install poetry==2.1.3
ENV POETRY_VIRTUALENVS_CREATE=false
COPY pyproject.toml poetry.lock ./
RUN poetry install --no-root --no-interaction --no-ansi

FROM python:3.12-slim
WORKDIR /app
RUN groupadd -r appgroup && useradd --no-log-init -r -g appgroup appuser
COPY --from=builder /usr/local/lib/python3.12/site-packages/ /usr/local/lib/python3.12/site-packages/
COPY ygg_torrent/ ./ygg_torrent/
RUN chown -R appuser:appgroup /usr/local/lib/python3.12/site-packages/
RUN chown -R appuser:appgroup /app
USER appuser

EXPOSE 8000
CMD ["python", "-m", "ygg_torrent"]