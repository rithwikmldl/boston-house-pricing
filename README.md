## **Boston House Prices Prediction and deployment using Heroku App**

### Software and Tools requirements

1. [GitHub Account](https://github.com)
2. [VS Code IDE](https://code.visualstudio.com/)
3. [HerokuAccount](https://heroku.com)
4. [GitCLI](https://git-scm.com/download/win)

### Create a new Environment

```
conda create -p venv python==3.10 -y
```

Create the Requirements file with name requirements.txt and use following command to install all the necessary packages

```
pip install -r requirements.txt
```


## Docker Commands


a. FROM - Set the name of the base image to use
```
FROM python:3.7
```

b. COPY - Copy files in the repository into the base image
```
# . --> current location to a location named as /app
COPY . /app
```

c. WORKDIR - Create the working directory
```
WORKDIR /app
``` 

d. RUN - parameter to the command
```
RUN pip install -r requirements.txt
``` 

e. EXPOSE - The port that the container should listen on
```
# $PORT is a placeholder and the server will automatically assign a port during deployment 
EXPOSE $PORT
``` 

f. CMD - Used to the run the application
```
# gunicorn help to run the python web application inside the Heroku cloud
# based on the incoming requests, it divides the work among the workers
# bind 0.0.0.0 is the local address in the heroku cloud

CMD gunicorn --workers=4 --bind 0.0.0.0:$PORT app:app
```