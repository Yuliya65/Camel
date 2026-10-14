FROM python:3.15-bookworm@sha256:dac6cb177b8c0f3dfeeaf57f0c6f708e1ca660ac8e952b0f4ac0c07972815385

RUN pip install uv
RUN groupadd -r appuser && useradd -r -g appuser appuser

WORKDIR /app/camel
COPY . .
RUN chown -R appuser:appuser /app/camel

RUN uv venv .venv --python=3.10 && \
    . .venv/bin/activate && \
    uv pip install -e ".[all, dev, docs]" && \
    pip install pre-commit mypy && \
    pre-commit install

ENV VIRTUAL_ENV=/app/camel/.venv
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

USER appuser

CMD ["bash"]
