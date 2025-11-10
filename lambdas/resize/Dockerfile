FROM public.ecr.aws/lambda/python:3.13

# install uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /uvx /bin/

# copy requirements file
COPY pyproject.toml ${LAMBDA_TASK_ROOT}/
RUN uv sync --no-install-project --no-editable

#Copy code
COPY handler.py ${LAMBDA_TASK_ROOT}/

#Edit Environment Variables
ENV VIRTUAL_ENV=/app/.venv
ENV PATH="${LAMBDA_TASK_ROOT}/.venv/bin:${PATH}"
ENV PYTHONPATH="${LAMBDA_TASK_ROOT}/.venv/lib/python3.13/site-packages"
ENV PYTHONDONTWRITEBYTECODE=1 PYTHONUNBUFFERED=1

# set the CMD to your handler
CMD ["handler.resize_handler"]
