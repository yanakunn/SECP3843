<a href="https://github.com/drshahizan/SECP3843/stargazers"><img src="https://img.shields.io/github/stars/drshahizan/SECP3843" alt="Stars Badge"/></a>
<a href="https://github.com/drshahizan/SECP3843/network/members"><img src="https://img.shields.io/github/forks/drshahizan/SECP3843" alt="Forks Badge"/></a>
<a href="https://github.com/drshahizan/SECP3843/pulls"><img src="https://img.shields.io/github/issues-pr/drshahizan/SECP3843" alt="Pull Requests Badge"/></a>
<a href="https://github.com/drshahizan/SECP3843/issues"><img src="https://img.shields.io/github/issues/drshahizan/SECP3843" alt="Issues Badge"/></a>
<a href="https://github.com/drshahizan/SECP3843/graphs/contributors"><img alt="GitHub contributors" src="https://img.shields.io/github/contributors/drshahizan/SECP3843?color=2b9348"></a>
![Visitors](https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2Fdrshahizan%2FSECP3843&labelColor=%23d9e3f0&countColor=%23697689&style=flat)


Don't forget to hit the :star: if you like this repo.

# Special Topic Data Engineering (SECP3843): Alternative Assessment

#### Name: Adrina Asyiqin Binti Md Adha
#### Matric No.: A20EC0174
#### Dataset: sales.json

## Question 5 (a)
### Ways to optimize performance when dealing with large volumes of JSON data
- `Load and preprocess data efficiently`
  
  Use streaming or chunked processing techniques to load and preprocess the JSON data in smaller portions rather than loading the entire dataset into memory at once. This can be done using libraries like pandas with the read_json function and specifying the lines=True parameter for reading JSON files line by line.
    ```py
    import pymongo
    import pandas as pd

    # Connect to MongoDB and retrieve data
    password = "Adrina857600"
    client = pymongo.MongoClient("mongodb+srv://cluster0.yvk5zzq.mongodb.net/", username="adrinaasyiqin", password=password)
    db = client["salesdatabase"]
    collection = db["salessample"]

    # Define the aggregation pipeline
    pipeline = [
        # Stage 1: Match documents based on criteria
        {"$match": {"date": {"$gt": "2022-01-01"}}},
        
        # Stage 2: Project only necessary fields
        {"$project": {"_id": 0, "date": 1, "storeLocation": 1, "customer": 1, "couponUsed": 1}}
    ]

    # Execute the aggregation pipeline
    cursor = collection.aggregate(pipeline)

    # Convert the cursor to a DataFrame
    df = pd.DataFrame(list(cursor))

    # Check the DataFrame
    print(df.head())
    df.info()

    ```
    ![image](https://github.com/drshahizan/SECP3843/assets/96984290/b03660a4-53ae-4aa4-8720-535924142231)



- `Optimize data retrieval`
  
  Retrieve only the required data for visualization instead of fetching the entire dataset. Use pagination or limit the number of records retrieved at a time based on user interactions. This can be done by incorporating server-side pagination or using API endpoints with pagination support.
    ```py
    import pymongo
    import pandas as pd

    # Connect to MongoDB and retrieve data
    password = "Adrina857600"
    client = pymongo.MongoClient("mongodb+srv://cluster0.yvk5zzq.mongodb.net/", username="adrinaasyiqin", password=password)
    db = client["salesdatabase"]
    collection = db["salessample"]

    # Create index on the frequently used field
    collection.create_index("date")

    # Define the query filter
    query = {"date": {"$gt": "2022-01-01"}}

    # Define the projection to retrieve only necessary fields
    projection = {"_id": 0, "date": 1, "storeLocation": 1, "customer": 1, "couponUsed": 1}

    # Retrieve data using optimized query and projection
    data = list(collection.find(query, projection))

    # Convert to DataFrame
    df = pd.DataFrame(data)

    # Check the DataFrame
    print(df.head())
    df.info()
    ```
    

- `Indexing`
  
  Create indexes on the fields that are frequently used for filtering or sorting. Indexing can significantly speed up query execution by allowing MongoDB to quickly locate the requested data. Use the create_index() method to create indexes on specific fields.
    ```py
    import pymongo
    import pandas as pd

    # Connect to MongoDB and retrieve data
    password = "Adrina857600"
    client = pymongo.MongoClient("mongodb+srv://cluster0.yvk5zzq.mongodb.net/", username="adrinaasyiqin", password=password)
    db = client["salesdatabase"]
    collection = db["salessample"]

    # Create index on the frequently used field
    collection.create_index("date")

    # Retrieve and filter data using MongoDB query
    query = {"date": {"$gt": "2022-01-01"}}
    data = list(collection.find(query))

    # Convert to DataFrame
    df = pd.DataFrame(data)

    # Check the DataFrame
    print(df.head())
    df.info()
    ```

- `Use data compression techniques`
  
  Compress the JSON data during transmission between the server and the client using compression algorithms like gzip or deflate. This reduces the network bandwidth required to transmit the data and improves the dashboard's loading time.

    ```py
    import pymongo

    # Connect to MongoDB
    password = "Adrina857600"
    client = pymongo.MongoClient("mongodb+srv://cluster0.yvk5zzq.mongodb.net/", username="adrinaasyiqin", password=password)
    db = client["salesdatabase"]
    collection = db["salessample"]

    # Enable compression for the collection
    collection.create_index([("date", pymongo.ASCENDING)], background=True)
    collection.create_index([("storeLocation", pymongo.ASCENDING)], background=True)
    collection.create_index([("customer", pymongo.ASCENDING)], background=True)
    collection.create_index([("couponUsed", pymongo.ASCENDING)], background=True)
    collection.create_index([("items", pymongo.ASCENDING)], background=True)
    collection.create_index([("purchaseMethod", pymongo.ASCENDING)], background=True)
    collection.create_index([("saleDate", pymongo.ASCENDING)], background=True)

    # Check compression status
    compression_status = collection.options().get('storageEngine', {}).get('wiredTiger', {}).get('configString', '').find('block_compressor')
    if compression_status != -1:
        print("Compression is enabled for the collection.")
    else:
        print("Compression is not enabled for the collection.")


    ```

## Question 5 (b)
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.


## Contribution 🛠️
Please create an [Issue](https://github.com/drshahizan/special-topic-data-engineering/issues) for any improvements, suggestions or errors in the content.

You can also contact me using [Linkedin](https://www.linkedin.com/in/drshahizan/) for any other queries or feedback.

[![Visitors](https://api.visitorbadge.io/api/visitors?path=https%3A%2F%2Fgithub.com%2Fdrshahizan&labelColor=%23697689&countColor=%23555555&style=plastic)](https://visitorbadge.io/status?path=https%3A%2F%2Fgithub.com%2Fdrshahizan)
![](https://hit.yhype.me/github/profile?user_id=81284918)
