FROM python:3.12.0
RUN pip install -U pip wheel setuptools && pip install black isort
WORKDIR /app
COPY . .
CMD python -m black --diff --line-length=120 --exclude "examples|tests" .
