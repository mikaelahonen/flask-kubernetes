# set base image (host OS)
FROM python:3.8-slim

#The working directory in Docker
WORKDIR /workdir

#Copy requirements from current directory to the code directory
COPY requirements.txt requirements.txt

#Install libraries
RUN pip install -r requirements.txt

#Environemnt variables to configure app
ENV FLASK_APP=app.run
ENV FLASK_RUN_HOST=0.0.0.0
ENV FLASK_ENV=development
ENV ENV=dev

#Open the port
EXPOSE 5200

#Copy the current directory . in the project to the workdir . in the image.
COPY . .
#Makes the app library available in the python console
RUN pip install -e .

CMD flask run -p 5200