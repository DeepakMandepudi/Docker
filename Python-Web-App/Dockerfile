FROM python:3.12-slim

WORKDIR /app

# Copy the requirements.txt file and install the dependencies
COPY requirements.txt /app
RUN pip install -r requirements.txt

# Copy the rest of the application code
COPY devops /app

# Specify the entry point and command for the application
ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]


# FROM ubuntu

# WORKDIR /app

# COPY requirements.txt /app
# COPY devops /app

# RUN apt-get update && \
#    apt-get install -y python3 python3-pip && \

# Use --break-system-packages If you want to bypass the restriction, you can add the --break-system-packages flag to the pip command. Note that this is not recommended unless you are sure it will not affect the stability of the environment.
#    pip install --break-system-packages -r requirements.txt

#    pip install -r requirements.txt && \
#    cd devops

# ENTRYPOINT ["python3"]
# CMD ["manage.py", "runserver", "0.0.0.0:8000"]
