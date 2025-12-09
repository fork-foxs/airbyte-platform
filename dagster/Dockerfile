FROM python:3.10-slim
RUN pip install dagster dagster-webserver dagster-postgres
RUN mkdir -p /opt/dagster_home
WORKDIR /opt/app
COPY workspace.yaml /opt/app/workspace.yaml
CMD ["dagster", "api", "grpc", "-h", "0.0.0.0", "-p", "3000"]

