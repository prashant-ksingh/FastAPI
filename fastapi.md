Fast API
- FastApi is a mordern, heigh-performance web framework for building APIs with python.
- made up using two python libraries Starlette and Pydentic.

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

Working of an api

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


## API Working in flask


Web Server(Gunicorn)  ----> SGI (WSGI->Werkzueg) ----> API Code(Sumchronous Endpoint)

@app.route("/predict", methods=["POST"])
def predict():
    json_data = request.get_json()
    data = InputData(** json_data)
    result = predict_sync(data)
    return jsonify(result)


-- WSGI--> this is of synchromous nature and blocking architechure, can lead to slower request


## API working in fastApi


15:47



