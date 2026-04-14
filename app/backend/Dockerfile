FROM python:3.11-slim

WORKDIR /app

# Install Poetry
RUN pip install poetry==1.7.1

# Copy dependency files from the project root
COPY ../../pyproject.toml ../../poetry.lock* /app/

# Configure Poetry and install dependencies
RUN poetry config virtualenvs.create false \
    && poetry install --no-interaction --no-ansi

# Copy the backend source code
COPY . /app

# Expose the port the app runs on
EXPOSE 8000

# Run the application
CMD ["uvicorn", "app.backend.main:app", "--host", "0.0.0.0", "--port", "8000"]
