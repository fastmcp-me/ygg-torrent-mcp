FROM python:3.12-slim AS builder
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY src/ ./src/

FROM python:3.12-slim
WORKDIR /app
RUN groupadd -r appgroup && useradd --no-log-init -r -g appgroup appuser
COPY --from=builder /usr/local/lib/python3.12/site-packages/ /usr/local/lib/python3.12/site-packages/
COPY --from=builder /app/src/ ./src/
RUN chown -R appuser:appgroup /app
USER appuser

EXPOSE 8000
CMD ["python", "-m", "src.mcp_server"]