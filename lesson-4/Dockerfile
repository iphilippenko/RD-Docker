FROM python:3.13-alpine
LABEL authors="irinashevcenko"

WORKDIR /src

COPY requirements.txt ./
RUN pip install -r requirements.txt

COPY /src ./

RUN addgroup -S myappgroup && adduser -S myappuser -G myappgroup && chown -R myappuser:myappgroup /src
USER myappuser

EXPOSE 8080

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8080"]
