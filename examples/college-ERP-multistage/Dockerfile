#####################################
##     Base Image 		   ##	
#####################################

FROM ubuntu AS build

WORKDIR /app

COPY requirements.txt /app/

COPY code /app/

RUN apt-get update && apt-get install -y python3 python3-pip python3-venv

#SHELL ["/bin/bash", "-c"]

RUN python3 -m venv venv1 && \
source venv1/bin/activate && \
pip install --no-cache-dir -r requirements.txt

############################################
# HERE STARTS THE MAGIC OF MULTI STAGE BUILD
############################################

FROM gcr.io/distroless/python3

COPY --from=build /app /app



EXPOSE 8000

CMD source venv1/bin/activate &&  manage.py runserver 0.0.0.0:8000



