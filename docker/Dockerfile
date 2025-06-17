FROM ghcr.io/astral-sh/uv:python3.13-bookworm-slim
COPY pyproject.toml uv.lock README.md ./
RUN uv sync --locked --no-editable
COPY ygg_torrent/ ./ygg_torrent/

EXPOSE 8000
CMD ["uv", "run", "--locked", "--no-sync", "-m", "ygg_torrent", "--mode", "sse"]