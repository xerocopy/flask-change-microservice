[![Flask Change Microservice Test](https://github.com/noahgift/flask-change-microservice/actions/workflows/main.yml/badge.svg)](https://github.com/noahgift/flask-change-microservice/actions/workflows/main.yml)

# flask-change-microservice
Small Flask Microservice that makes change

*Coursera Lab:  duke-coursera-ccb-lab2*

![coursera-lab](https://user-images.githubusercontent.com/58792/108137449-df0e0300-7089-11eb-8b11-74f478b71d11.png)


## Invoke Endpoint

* Create virtualenv and source it: `python3 -m venv ~/.fcm && source ~/.venv/bin/fcm`
* Install and Test:  `make all`
* Run it:  `python app.py`
* Invoke it.  Options include curl, Postman, httpie.  These methods are documented below


### Curl

`curl http://127.0.0.1:8080/change/1/34`

```bash
[
  {
    "5": "quarters"
  },
  {
    "1": "nickels"
  },
  {
    "4": "pennies"
  }
]
```
### httpie

[Installation of httpie](https://httpie.io/docs#installation)

`http 127.0.0.1:8080/change/1/34`

```bash
HTTP/1.0 200 OK
Content-Length: 90
Content-Type: application/json
Date: Tue, 16 Mar 2021 16:49:11 GMT
Server: Werkzeug/1.0.1 Python/3.9.0

[
    {
        "5": "quarters"
    },
    {
        "1": "nickels"
    },
    {
        "4": "pennies"
    }
]
```


### Postman

[Install Postman](https://www.postman.com)
![postman](https://user-images.githubusercontent.com/58792/111342614-00461d00-8651-11eb-8433-d7d91d3e48b4.png)

### Requests

The [Python requests library](https://requests.readthedocs.io/en/latest/user/quickstart/) allows you to invoke a request as a "one-liner" or a script.

`python -c "import requests;r=requests.get('http://127.0.0.1:8080/change/1/34');print(r.json())"`

Result:

`[{'5': 'quarters'}, {'1': 'nickels'}, {'4': 'pennies'}]`

## Loadtest with Locust

* [Install Locust](https://github.com/locustio/locust)
* Create a `locustfile.py`
* Run loadtests
![Screen Shot 2021-03-16 at 3 02 59 PM](https://user-images.githubusercontent.com/58792/111367175-d7328600-866a-11eb-9a4d-3429710593ea.png)
![Screen Shot 2021-03-16 at 3 02 35 PM](https://user-images.githubusercontent.com/58792/111367176-d7328600-866a-11eb-9856-928d42e65a9a.png)
![Screen Shot 2021-03-16 at 3 01 22 PM](https://user-images.githubusercontent.com/58792/111367178-d7cb1c80-866a-11eb-8c29-6440a6179544.png)


# Turn the flask-change-microservice into a kubernetes project

#### Create new Assets in Project:

1. Makefile
2. Dockerile
3. app.py (no change)
4. kube-hello-change.yaml


#### create new environment
python3 -m venv ~/.kube-hello && source ~/.kube-hello/bin/activate

run make all


#### Build and Run Docker Container
1. Install Docker Desktop

2. docker build -t flask-change:latest . or run make build which has the same command.

 to confirm the docker file: docker image ls

3. docker run -p 8080:8080 flask-change or run make run

4. In a separate terminal invoke the web service via curl, or run make invoke which has the same command

curl http://127.0.0.1:8080/change/1/34

[
  {
    "5": "quarters"
  },
  {
    "1": "nickels"
  },
  {
    "4": "pennies"
  }
]

#### Running Kubernetes Locally !!! (Make comment not working well On a local machine. when run the app in local use http://localhost:8080/ to view the services)

5. Verify Kubernetes is working via docker-desktop context

(.kube-hello) ➜  kubernetes-hello-world-python-flask git:(main) kubectl get nodes
NAME             STATUS   ROLES    AGE   VERSION
docker-desktop   Ready    master   30d   v1.19.3

6. Run the application in Kubernetes using the following command which tells Kubernetes to setup the load balanced service and run it:

kubectl apply -f kube-hello-change.yaml or run make run-kube which has the same command

7. verify the container is Running

kubectl get pods

8. describe the load balanced service:
kubectl describe services

9. invoke the endpoint to curl it:
curl http://127.0.0.1:8080/change/1/34



<<<<<<< HEAD
kubectl apply -f kube-hello-change.yaml or run make run-kube which has the same command




### Load testing with locust (https://locust.io/)

#### Curl
curl http://127.0.0.1:8080/change/1/34


#### httpie
install: python -m pip install --upgrade pip wheel &&  python -m pip install httpie

http 127.0.0.1:8080/change/1/34

#### Postman
login at: https://web.postman.co/workspace/My-Workspace~8c33987b-03a6-45c1-8225-c1f35faa1994/request/create?requestId=9dfd525b-f75d-42eb-b622-136997629b4b

put the url http://ec2-3-92-96-168.compute-1.amazonaws.com:8080/change/1/34 in get 

#### Python request Library allows you to invoke a request as a "one-liner" or a script.
python -c "import requests;r=requests.get('http://127.0.0.1:8080/change/1/34');print(r.json())"

Result:

[{'5': 'quarters'}, {'1': 'nickels'}, {'4': 'pennies'}]


#### Locust
install locust

create a locustfile.py

run locust 

if recieve error as follows ( File "/home/ec2-user/.kube-hello/lib64/python3.7/site-packages/locust/web.py", line 102, in __init__  app.jinja_options["extensions"].append("jinja2.ext.do")
KeyError: 'extensions'), click the last line of error message linked to the web.py

replace app.jinja_options['extensions'].append('jinja2.ext.do') with app.jinja_env.add_extension('jinja2.ext.do')

starting interface at http://ec2-3-92-96-168.compute-1.amazonaws.com:8089/


=======
#### to clean up the deployment do the following:
 kubectl delete deployment hello-python
>>>>>>> f942dc45632698a88f05560a6dfdb9fdc4d208ee
