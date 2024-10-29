FROM python:3.10-alpine
RUN apk update && apk add curl

WORKDIR /app
ENV PORT=3002
ADD tokenizer.py /app/tokenizer.py
ADD requirements.txt /app/requirements.txt
RUN pip install -i https://mirrors.aliyun.com/pypi/simple --upgrade pip
RUN pip install --root-user-action=ignore -i https://mirrors.aliyun.com/pypi/simple -r requirements.txt
HEALTHCHECK --interval=5s --timeout=30s --retries=3 \
CMD curl -f -X POST -H "Content-Type: application/json" -d "{\"role\":\"user\", \"content\":\"hello\"}" http://localhost:${PORT}/tokenizer/gpt-3.5-turbo || exit 1
CMD ["sh", "-c", "nuxt --port ${PORT} --module tokenizer.py --workers 2"]