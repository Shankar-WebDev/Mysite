FROM python:3.12-slim

# Set the working directory to /app
WORKDIR /app

# Copy the requirements file and install dependencies
COPY pyproject.toml requirement.txt ./
RUN pip wheel --no-cache-dir --no-deps --wheel-dir wheels -r requirement.tx

# Copy your application code into the container
COPY src src

RUN pip wheel --no-cache-dir --no-deps --wheel-dir wheels .


FROM python:3.12-slim AS runner

COPY --from=builder /app/wheels / wheels
RUN pip install -no-cache /wheels/* && -rf /wheels

# Expose the port the app will run on
EXPOSE 8000

# Set the command to run the FastAPI app using uvicorn
CMD ["uvicorn", "mysite.main:app", "--host", "0.0.0.0", "--port", "8000"]
