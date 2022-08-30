##Install it:
```python
pip install flatten-everything
```

##Import it: 

```python
from flatten_everything import flatten_everything, ProtectedDict,ProtectedList,ProtectedTuple,ProtectedSet
```

##Use it:
```python

#Let's create some random data



import numpy as np

from collections import UserDict, OrderedDict

import pandas as pd

a = np.array([2, 3, 4], dtype=np.uint32)

b = np.array([5, 6, 7], dtype=np.uint32)

data = { # https://www.geeksforgeeks.org/converting-nested-json-structures-to-pandas-dataframes/

 "company": "XYZ pvt ltd",

 "location": "London",

 "info": {

 "president": "Rakesh Kapoor",

 "contacts": {"email": "contact@xyz.com", "tel": "9876543210"},

 },

}

data2 = [ # https://www.geeksforgeeks.org/converting-nested-json-structures-to-pandas-dataframes/

 {

 "id": "001",

 "company": "XYZ pvt ltd",

 "location": "London",

 "info": {

 "president": "Rakesh Kapoor",

 "contacts": {"email": "contact@xyz.com", "tel": "9876543210"},

 },

 },

 {

 "id": "002",

 "company": "PQR Associates",

 "location": "Abu Dhabi",

 "info": {

 "president": "Neelam Subramaniyam",

 "contacts": {"email": "contact@pqr.com", "tel": "8876443210"},

 },

 },

]

dataf = pd.json_normalize(data)

dicti2 = {

 "name": {"name": "John", "age": "27", "sex": "Male"},

 "Peter2": {"name": "Marie", "age": "22", "sex": "Female"},

 "sdfsdf": {"name": "Luna", "age": "24", "sex": "Female"},

 "Peter": {"name": "Peter", "age": "29", "sex": "Male"},

}

dicti = {

 "name": {"name": "John", "age": "27", "sex": "Male"},

 "Peter2": {"name": "Marie", "age": "22", "sex": "Female"},

 "sdfsdf": {"name": "Luna", "age": "24", "sex": "Female"},

 "Peter": {"name": Peter", "age": "29", "sex": "Male"},

}

odi = OrderedDict(dicti2)

ada = UserDict(dicti2)

testlistnotprotected1 = {

 "mytest": [

 ["dd", "xxaa"],

 [[[[(data, 111, {33, 44, 22})]]], [data2]],

 dataf,

 {"blabla": data2},

 "stads",

 (444, 4),

 21.2,

 ["sda", "sadfrs"],

 ("bababa", 44, [111, 111, 111]),

 dicti,

 a,

 b,

 ["colkey"],

 odi,

 ada,

 np.arange(27).reshape((3, 3, 3)),

 ]

}

flattened1 = list((flatten_everything(testlistnotprotected1)))



#output:



['dd',

 'xxaa',

 'XYZ pvt ltd',

 'London',

 'Rakesh Kapoor',

 'contact@xyz.com',

 '9876543210',

 111,

 33,

 44,

 22,

 '001',

 'XYZ pvt ltd',

 'London',

 'Rakesh Kapoor',

 'contact@xyz.com',

 '9876543210',

 '002',

 'PQR Associates',

 'Abu Dhabi',

 'Neelam Subramaniyam',

 'contact@pqr.com',

 '8876443210',

 'XYZ pvt ltd',

 'London',

 'Rakesh Kapoor',

 'contact@xyz.com',

 '9876543210',

 '001',

 'XYZ pvt ltd',

 'London',

 'Rakesh Kapoor',

 'contact@xyz.com',

 '9876543210',

 '002',

 'PQR Associates',

 'Abu Dhabi',

 'Neelam Subramaniyam',

 'contact@pqr.com',

 '8876443210',

 'stads',

 444,

 4,

 21.2,

 'sda',

 'sadfrs',

 'bababa',

 44,

 111,

 111,

 111,

 'John',

 '27',

 'Male',

 'Marie',

 '22',

 'Female',

 'Luna',

 '24',

 'Female',

 'Peter',

 '29',

 'Male',

 2,

 3,

 4,

 5,

 6,

 7,

 'colkey',

 'John',

 '27',

 'Male',

 'Marie',

 '22',

 'Female',

 'Luna',

 '24',

 'Female',

 'Peter',

 '29',

 'Male',

 'name',

 'Peter2',

 'sdfsdf',

 'Peter',

 0,

 1,

 2,

 3,

 4,

 5,

 6,

 7,

 8,

 9,

 10,

 11,

 12,

 13,

 14,

 15,

 16,

 17,

 18,

 19,

 20,

 21,

 22,

 23,

 24,

 25,

 26]



#You can also protect lists, dicts, tuples and sets from getting flattened



testlistprotected2 = {

    "mytest": [

        ["dd", "xxaa"],

        [[[[(data, 111, {33, 44, 22})]]], [data2]],

        dataf,

        ProtectedDict({"blabla": data2}),

        "stads",

        (444, 4),

        21.2,

        ProtectedList(["sda", "sadfrs"]),

        ProtectedTuple(("bababa", 44, [111, 111, 111])),

        dicti,

        a,

        b,

        ["colkey"],

        odi,

        ada,

        np.arange(27).reshape((3, 3, 3)),

    ]

}



flattened2 = list((flatten_everything(testlistprotected2)))

#output:

['dd',

 'xxaa',

 'XYZ pvt ltd',

 'London',

 'Rakesh Kapoor',

 'contact@xyz.com',

 '9876543210',

 111,

 33,

 44,

 22,

 '001',

 'XYZ pvt ltd',

 'London',

 'Rakesh Kapoor',

 'contact@xyz.com',

 '9876543210',

 '002',

 'PQR Associates',

 'Abu Dhabi',

 'Neelam Subramaniyam',

 'contact@pqr.com',

 '8876443210',

 'XYZ pvt ltd',

 'London',

 'Rakesh Kapoor',

 'contact@xyz.com',

 '9876543210',

 {'blabla': [{'id': '001',

    'company': 'XYZ pvt ltd',

    'location': 'London',

    'info': {'president': 'Rakesh Kapoor',

     'contacts': {'email': 'contact@xyz.com', 'tel': '9876543210'}}},

   {'id': '002',

    'company': 'PQR Associates',

    'location': 'Abu Dhabi',

    'info': {'president': 'Neelam Subramaniyam',

     'contacts': {'email': 'contact@pqr.com', 'tel': '8876443210'}}}]},

 'stads',

 444,

 4,

 21.2,

 ['sda', 'sadfrs'],

 ('bababa', 44, [111, 111, 111]),

 'John',

 '27',

 'Male',

 'Marie',

 '22',

 'Female',

 'Luna',

 '24',

 'Female',

 'Peter',

 '29',

 'Male',

 2,

 3,

 4,

 5,

 6,

 7,

 'colkey',

 'John',

 '27',

 'Male',

 'Marie',

 '22',

 'Female',

 'Luna',

 '24',

 'Female',

 'Peter',

 '29',

 'Male',

 'name',

 'Peter2',

 'sdfsdf',

 'Peter',

 0,

 1,

 2,

 3,

 4,

 5,

 6,

 7,

 8,

 9,

 10,

 11,

 12,

 13,

 14,

 15,

 16,

 17,

 18,

 19,

 20,

 21,

 22,

 23,

 24,

 25,

 26]
 
 ```
