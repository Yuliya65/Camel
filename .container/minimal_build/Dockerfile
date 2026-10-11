FROM python:3.14-bookworm@sha256:7ee7e4d4fb42c3ad45b8fdc473b64ec69c3cf6e80ae5d52f6fa55f77fac29027

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
