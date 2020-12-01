# File-based-key-value-datastore-with-CRD-operations
Build a file-based key-value data store that supports the basic CRD (create, read, and delete)
operations. This data store is meant to be used as a local storage for one single process on one
laptop. The data store must be exposed as a library to clients that can instantiate a class and work
with the data store.

# Datastore supports the functional requirements as mentioned in problem statement.
1. It can be initialized using an optional file path. If one is not provided, it will reliably
create itself in a reasonable location on the laptop.
2. A new key-value pair can be added to the data store using the Create operation. The key
is always a string - capped at 32chars. The value is always a JSON object - capped at
16KB.
3. If Create is invoked for an existing key, an appropriate error must be returned.
4. A Read operation on a key can be performed by providing the key, and receiving the
value in response, as a JSON object.
5. A Delete operation can be performed by providing the key.
6. Every key supports setting a Time-To-Live property when it is created. This property is
optional. If provided, it will be evaluated as an integer defining the number of seconds
the key must be retained in the data store. Once the Time-To-Live for a key has expired,
the key will no longer be available for Read or Delete operations.
7. Appropriate error responses must always be returned to a client if it uses the data store in
unexpected ways or breaches any limits.

# Datastore will also support the non-functional requirements mentioned in problem statement.
1. The size of the file storing data must never exceed 1GB.
2. More than one client process cannot be allowed to use the same file as a data store at any
given time.
3. A client process is allowed to access the data store using multiple threads, if it desires to.
The data store must therefore be thread-safe.
4. The client will bear as little memory costs as possible to use this data store, while
deriving maximum performance with respect to response times for accessing the data
store.

# Environment Required to run this
1. Operating system: Ubuntu 18.04
2. Python: Python3.6 or higher
3. Dependencies installation : `python3 -m pip install -r requirements.txt`
4. Run `app.py` to run the backend server.
    1. To start datastore from default file location, run `python3 app.py`
    2. To start datastore from user defined file location, run `python3 app.py --datastore=<absolute_path_of_your_datastore>` 

# REST API CRD Operations execution through POSTMAN
To use this API I have used a tool called Postman for sending requests and getting responses.
1. Create data in DataStore with Postman- link is `http://localhost:5000/datastore/create` and select raw data option in Postman and enter data as
    {
    "abc": {
        "data1": "value1",
        "data2": "value2",
        "data3": "value3",
        "Time-To-Live": 5000
        }
    }
2. Read data from datastore - Request type: `GET`,link is `http://localhost:5000/datastore/read`, key=`abc`
3. Delete data from datastore - Request type: `DELETE`,link is `http://localhost:5000/datastore/delete`, key=`abc`

# Test Environment Setup
1. To test the Create operation of data in datastore, run `python3 test_create_data.py` for default datastore or run `python3 test_create_data.py --datastore=<absolute_path_of_your_datastore>` for custom datastore location.
2. To test the Read operation of data in datastore, run `python3 test_read_data.py` for default datastore or run `python3 test_read_data.py --datastore=<absolute_path_of_your_datastore>` for custom datastore location.
3. To test the Delete operation of data in datastore, run `python3 test_delete_data.py` for default datastore or run `python3 test_delete_data.py --datastore=<absolute_path_of_your_datastore>` for custom datastore location.

