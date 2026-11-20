FROM python:3.10-bookworm@sha256:f72a86806f92fe13a49f49aeca1db0b19ea5cf4a0470b842a01b0e14314945b8

RUN pip install uv
RUN groupadd -r appuser && useradd -r -g appuser appuser

COPY . /app/camel
WORKDIR /app/camel
RUN chown -R appuser:appuser /app/camel

RUN uv venv .venv --python=3.10 && \
    . .venv/bin/activate && \
    uv pip install -e ".[all, dev, docs]" && \
    pip install pre-commit mypy

USER appuser

CMD ["tail", "-f", "/dev/null"]
