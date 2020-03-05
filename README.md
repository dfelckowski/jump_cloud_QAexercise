# jump_cloud_QAexercise

Test Cases- Jump Cloud Exercise


***POST/GET  Curl Commands***
——————————————————————

POST with proper port assignment.

Prerequisites:
-Port assigned (example PORT=8088)

- Execute curl command (curl -X POST -H "application/json" -d '{"password":"angrymonkey"}' http://127.0.0.1:8088/hash), Verify port 8088 works correctly. 
- POST command should work properly.


——————————————————————

POST without proper port assignment.

Prerequisites:
-Port assigned is different than curl command port (example PORT=8090) 

- Execute curl command (curl -X POST -H "application/json" -d '{"password":"angrymonkey"}' http://127.0.0.1:8088/hash), Verify port 8088 listed in curl command does not connect properly. 
- POST command should not connect.

——————————————————————

POST without a port assignment.

Prerequisites:
-Do not assign port before running this test.

- Execute curl command (curl -X POST -H "application/json" -d '{"password":"angrymonkey"}' http://127.0.0.1:8088/hash), 
- POST command should not connect, and cause crash according to the assignment document.

——————————————————————

POST accepting password

Prerequisites:
-Port assigned (example PORT=8088)

- Execute curl command (curl -X POST -H "application/json" -d '{"password":"angrymonkey"}' http://127.0.0.1:8088/hash)
- POST command should work properly, It should then wait 5 seconds and compute the password hash. The hashing algorithm should be SHA512.
- Response will be ’42’

——————————————————————

POST multiple passwords simultaneously

Prerequisites:
-Port assigned (example PORT=8088)

- Execute curl command (curl -X POST -H "application/json" -d '{"password":"angrymonkey"}' http://127.0.0.1:8088/hash)
- Repeat curl command numerous times.
- Multiple POST commands should work properly, Each attempt should wait 5 seconds and compute the password hash. (The hashing algorithm should be SHA512)
 - Response will be ’42’ for each attempt.
- Verify the number of attempts appear properly in GET /stats (curl http://127.0.0.1:8088/stats)

——————————————————————

GET to /hash accepts Job Identifier

Prerequisites:
-Port assigned (example PORT=8088)

-Execute curl command (curl -H "application/json" http://127.0.0.1:8088/hash/1),
-It should return the base64 encoded password hash for the corresponding POST request. (Example: > zHkbvZDdwYYiDnwtDdv/FIWvcy1sKCb7qi7Nu8Q8Cd/MqjQeyCI0pWKDGp74A1g==)

——————————————————————

GET to /stats accepts Job Identifier

Prerequisites:
-Port assigned (example PORT=8088)

-Execute curl command (curl http://127.0.0.1:8088/stats)
-This should not accept any data.
-Response should return JSON for total hash requests since started & average time of hash request in ms. (Example: > {"TotalRequests":3,"AverageTime":5004625})

——————————————————————

Test Password Hashing application on multiple OS options

Prerequisites:
-Port assigned using Ubuntu 16.04 ● Mac OS X - Sierra, High Sierra ● Windows 10 (example 8088)
-Appropriate applications for each OS installed.

-Verify above test cases work under Ubuntu 16.04
-Verify above test cases work under Mac OS X - Sierra, High Sierra
-Verify above test cases work under Ubuntu Windows 10

——————————————————————

Shutdown with proper port assignment

Prerequisites:
-Port assigned (example PORT=8088)

-Execute curl command (curl -X POST -d ‘shutdown’ http://127.0.0.1:8088/hash).
-Response should return (> 200 Empty Response)

——————————————————————

Shutdown with proper port assignment

Prerequisites:
-Port assigned (example PORT=8088)

-Execute curl command (curl -X POST -d ‘shutdown’ http://127.0.0.1:8088/hash).
-Response should return (> 200 Empty Response)
-Application should shut down.

——————————————————————

Shutdown without proper port assignment.

Prerequisites:
-Port assigned is different than curl command port (example PORT=8090)

-Execute curl command (curl -X POST -d ‘shutdown’ http://127.0.0.1:8088/hash).
-Shutdown should not work properly, since port does not match initial assigned port.

——————————————————————

Shutdown with ongoing hash commands still running.

Prerequisites:
-Port assigned (example PORT=8088)
-Has requests need to be running during shutdown process.

-Execute curl command (curl -X POST -d ‘shutdown’ http://127.0.0.1:8088/hash).
-Verify hash commands finish before shutdown procedure takes place.
-Verify new hash requests will not work while shutdown process has started.
-Response should return (> 200 Empty Response)
-Application should shut down.



*************************************************************************************************************************

Defects/Questions

-Post command does not give a response back (documentation shows 42 when running curl command)

-Shutdown curl gets Malformed input message & never shuts down (should get 200 Empty Response after shutdown)

-Get /hash information response different than documentation (see below)

(From request) 	NN0PAKtieayiTY8/Qd53AeMzHkbvZDdwYYiDnwtDdv/FIWvcy1sKCb7qi7Nu8Q8Cd/MqjQeyCI0pWKDGp74A1g==
(From documentation)                                                  zHkbvZDdwYYiDnwtDdv/FIWvcy1sKCb7qi7Nu8Q8Cd/MqjQeyCI0pWKDGp74A1g==

-Average time in hash request is 9+ seconds (documentation shows 5 seconds)




Comments


-Are there password restrictions upon creation (capital letter, symbols, length?)
-When app is launched, it doesn’t show that it is doing anything, should it mention it’s awaiting http connections?
-Should app log any other info besides the attempted shutdown?
-The hashing algorithm should be SHA512. Tried using an online tool to verify input/output? 
-Cannot test the rest of shutdown test cases with open shutdown defect above.




