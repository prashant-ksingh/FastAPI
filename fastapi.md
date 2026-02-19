# Fast API
L-2
#### - FastApi is a mordern, heigh-performance web framework for building APIs with python.

#### - made up using two python libraries Starlette and Pydentic.

Starlette
- Starlette manages how your API recives requests and sends back response.

Pydentic
- Pydentic is data validation library(by default no data validation and type hunting availabe in python).
- Pydentic is used to check if the data coming into your API is correct and in the right format.


In the older python frameworks 
- there was performance issue, response time was slow and latancy issues(these are not good for industry grade app)
- there was a lot of unneccesary code to write 

Philosophy of FastAPI
- Fast to run 
-Fast to code

why fastapi id fat to run 

## Working of an API

web Server ------------------------------->  SGI -------------------------------> API Code

POST /predict HTTP/1.1                                     
Host: api.example.com                
Content-Type: application/json        
Content-Length: 45                                       

    {
        "feature": 5.2,
        "feature": 3.1
    }

SGI(Server Gateway Interface) --> Establishes two way communication
- Converts the request data to below format

    Request.method-->"POST"
    Request.url--> "/predict"
    Request.json()--> {"feature1": 5.2,"feature2":3.1 }


- Now the API code genrates the output

"prediction": 8.3

-  SGI angain changes to the data into request body

    HTTP/1.1 200 OK
    Content-Type application/json
    {
        "prediction":8.3
    }

### WSGI - -- a specification that standardizes hoe web server and python applications frameworks communicate  (WSGI & ASGI)

## API Working in flask


Web Server(Gunicorn)  ----> SGI (WSGI->Werkzueg) ----> API Code(Sunchronous Endpoint)

code is also synchronous

    @app.route("/predict", methods=["POST"])
    def predict():
        json_data = request.get_json()
        data = InputData(** json_data)
        result = predict_sync(data)
        return jsonify(result)


-- WSGI--> this is of synchronous nature and blocking architechure, can lead to slower request


### ASGI - is a newer, Asynchronous interface that's better suited for mordern web applications like those using Websockets or real_time features


## API working in fastApi

Different in three aspacts in comparison to flask

1- Async server gateway

2- library is Starleete 

3- Uvicorn web server is used

the code is also writen in asynchronous way

Web Server(Uvicorn)  ----> SGI (ASGI->Starlette) ----> API Code(Asynchronous Endpoint)

    @app.post("/predict")
    async def predict(data : InputData):
        result = await predict_async(data)
        return result


### Why Fast API is fast to code?
1- Automatic input vlidation(varibales are created dynamically in python, makes validation important)

2- Auto-Genrated interactive Document

3- Seamless integration with mordern Ecosystem(ML/DL libraries, OAuth, jwt, SQL Alchemy, Docker, Kuberntes etc.)

# Installing FastAPI
check if python is available

    python --version

create a virtual envirnment 

    python -m venv venv

Activate the envirnment 

    For windows - venv/Scripts/activate
    For Mac - source .venv/bin/activate

install Dependencies and fast api

    pip install fastapi uvicorn pydentic

create a file main.py and write a hello world code in it 

    from fastapi import FastAPI

    app = FastAPI()

    @app.get("/")
    def hello():
        return{ 'message':"Hello World !!"}

run you program using uvicorn (relaod will reaload your code with every change)

    uvicorn main:app --reload

To Acess api endpoints open the below in you browser

    http://127.0.0.1:8000/
    http://127.0.0.1:8000/about

To acress auto genrated docs by Fast API

    http://127.0.0.1:8000/docs

    can interact with docs using "Try it out" button then click "Execute" button

L-3

## HTTP Methods

software ---------> static software(e.g. calander)

   |
   -------->Dynamic software(ms word)


(Types of intraction with s/w) ----> CRUD

    SERVER ----------------->CLIENT

           <------------------
               HTTP Protocol

Types of interaction (HTTP Method) :

     GET  POST PUT PATCH DELETE

### HTTP Status code

are 3 digit numbers returned in the response by a web browser server (like FastAPI) to indicate the result of a client's request(like from a browser or API consumer)

They help the client (browser, frontend, mobile app etc.) understand:
- whether the request was successful.
- whether something went wrong.
- and what kind of issue  occurred(if any)

2xx - success - the request was successfully received and processed
3xx - redirection- Further action needs to be taken
4xx- Client Error - Something is wrong with the request from the client
5xx - Server Error - Something went wrong on the server side

can go and check some famous status code to get more understanding

## HTTP Exception


HTTPException is a special built-in exception in FASTAPI used to return an custom HTTP error Responses when something goes wrong in your API
instead of returning a normal JSON or crashing the server, you can gracefully raise an error with:
a proper HTTP status code(like 404, 403 etc)
a custom error message
(optional) extra headers


## The path() function

The path() function in FastAPI is used to to provide metadata, validation rule and documentation hints for path parameters in your API endpoints

Title , Description
Example  ge, gt, le, lt    min_length, max_length, regex

