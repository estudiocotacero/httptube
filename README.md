httptube
========

Asynchronous HTTP Server based on beanstalk


The idea is simple, imagine that someone reaches your API with a call like

curl "http://localhost:23579/api1/sessions/12314123123/stations?pretty=true"

it creates a job to a beanstalk tube "sessions"

`{"method":"get", "uri":"/api1/sessions/12314123123/stations",
 "parameter": "pretty=true",
 "tube" : {
    "tubeSessionId":"0f66d46081397aa7d41a51a7789fa5af",
    "host":"myserver.com",
    "port":11300,
    "tube":"httpTubeAnswers_123812312" }
  }
}`
 
when the job is processed, you must send the answer to the beanstalk tube (myserver.com:11300, tube httpTubeAnswers_123812312) with the field "tubeSessionId".

`{
 "tubeSessionId":"0f66d46081397aa7d41a51a7789fa5af",
 "keepOpen": true,
 "answer" : {
    "status":"success",
    "stations":[ ] }
}`

