FROM python:3.13-alpine
LABEL authors="irinashevcenko"

WORKDIR /src

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

COPY /src ./

RUN addgroup -S myappgroup \
    && adduser -S myappuser -G myappgroup \
    && chown -R myappuser:myappgroup /src
USER myappuser

EXPOSE 8080

HEALTHCHECK --interval=10s --timeout=5s --retries=5 --start-period=10s \
  CMD python -c "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8080/healthz')"

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8080"]
