FROM python:3.10-bookworm@sha256:94c362db08c5b38857943d31b10558ff1856e918605c474d205d72a534929d4e

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
