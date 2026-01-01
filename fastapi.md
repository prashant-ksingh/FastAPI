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

web Server ------------------------------->  SGI -------------------------------> API Code

POST /predict HTTP/1.1                                     
Host: api.example.com                
Content-Type: application/json        
Content-Length: 45                                       

{
    "feature": 5.2,
    "feature": 3.1
}

Request.method-->"POST"
Request.url--> "/predict"
Request.json()--> {"feature1": 5.2,"feature2":3.1 }


"preediction": 8.3


HTTP/1.1 200 OK
Content-Type application/json
{
    "prediction":8.3
}


