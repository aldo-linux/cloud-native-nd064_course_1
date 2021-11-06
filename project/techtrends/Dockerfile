FROM python:2.7
LABEL maintainer="Aldo Gonzalez"

WORKDIR /usr/src/app
ADD . .
RUN pip install --upgrade pip
RUN pip install --no-cache-dir -r ./requirements.txt
RUN python init_db.py
EXPOSE 3111

# command to run on container start
CMD [ "python", "app.py" ]
