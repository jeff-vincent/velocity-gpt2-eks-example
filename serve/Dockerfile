FROM tensorflow/tensorflow:latest-gpu

COPY main.py .

# Add deadsnakes repo
RUN apt update
RUN apt-get install software-properties-common -y
RUN add-apt-repository ppa:deadsnakes/ppa -y

# Install Python 3.10
RUN apt update && apt install -y python3.10 python3.10-distutils
RUN curl -sS https://bootstrap.pypa.io/get-pip.py | python3.10

RUN apt-get install git -y
RUN pip install git+https://github.com/keras-team/keras-nlp.git -q


# Replace python shell with python3.10
RUN unlink /usr/bin/python
RUN ln -s /usr/bin/python3.10 /usr/bin/python

RUN pip install fastapi uvicorn boto3

CMD uvicorn main:app --host 0.0.0.0 --port 8000
