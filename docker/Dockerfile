FROM python:3.10 as base

WORKDIR /app
ADD pyproject.toml .
ADD requirements.txt .
RUN pip install . && rm pyproject.toml requirements.txt
ENV PYTHONPATH=/app

FROM base as github_app
ADD pr_agent pr_agent
CMD ["python", "pr_agent/servers/github_app.py"]

FROM base as bitbucket_app
ADD pr_agent pr_agent
CMD ["python", "pr_agent/servers/bitbucket_app.py"]

FROM base as github_polling
ADD pr_agent pr_agent
CMD ["python", "pr_agent/servers/github_polling.py"]

FROM base as test
ADD requirements-dev.txt .
RUN pip install -r requirements-dev.txt && rm requirements-dev.txt
ADD pr_agent pr_agent
ADD tests tests

FROM base as cli
ADD pr_agent pr_agent
ENTRYPOINT ["python", "pr_agent/cli.py"]
