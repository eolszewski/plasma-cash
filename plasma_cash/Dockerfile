FROM python:3.6-alpine

# work directory
ADD . /usr/src/plasma_cash
WORKDIR /usr/src/plasma_cash

# install bash, git, openssh
RUN apk update && apk upgrade && apk add --no-cache bash git openssh

# install requirements
RUN pip install -r requirements.txt

# start plasma chain
RUN FLASK_APP=./child_chain FLASK_ENV=development flask run --port=8546 &

# launch demo
CMD ["python", "demo.py"]