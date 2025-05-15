FROM python:3.10 as builder

WORKDIR /app

COPY pyproject.toml .
RUN pip install --user --no-cache-dir -e .

COPY src/ src/
COPY tests/ tests/

FROM python:3.10-slim

WORKDIR /app

COPY --from=builder /root/.local /root/.local
COPY --from=builder /app /app

ENV PYTHONPATH=/app
ENV PATH=/root/.local/bin:$PATH

EXPOSE 8109

CMD ["uvicorn", "src.main:app", "--host", "0.0.0.0", "--port", "8109"]

