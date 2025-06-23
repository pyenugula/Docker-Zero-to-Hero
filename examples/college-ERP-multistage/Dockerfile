#####################################
##     Base Image 		   ##
#####################################

FROM ubuntu AS build

WORKDIR /app

COPY requirements.txt /app/
COPY code /app/

RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-venv && \
    rm -rf /var/lib/apt/lists/*  # Clean up to reduce image size

# Create a virtual environment and install dependencies
RUN pip install --no-cache-dir -r requirements.txt

############################################
# HERE STARTS THE MAGIC OF MULTI STAGE BUILD
############################################

# Use a standard Python base image with a shell
FROM gcr.io/distroless/python3  # Choose a version that fits your needs

# Copy the application code and virtual environment
COPY --from=build /app /app

# Set the working directory
WORKDIR /app

EXPOSE 8000

# Use the entrypoint to run the application
CMD ["python3", "/app/manage.py", "runserver", "0.0.0.0:8000"]

