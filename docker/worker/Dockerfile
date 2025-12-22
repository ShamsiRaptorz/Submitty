FROM python:3.10-slim

WORKDIR /app

# Install dependencies
RUN pip install psycopg2-binary

# Copy worker scripts (simulation)
COPY . /app

CMD ["python3", "-c", "print('Autograding worker running')"]
