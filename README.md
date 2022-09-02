# la-deep-get
Function to get value that is deep inside another structure.  

# install
`pip install la-deep-get`  

# syntax
```python
dget(structure, *args, default=None)
```  
`structure` - Structure to go through  
`*args` - Each field to be passed as key  
`default` - The value to return in case it fail to access any of the keys (default is `None`)  

# example
Let's say that you have dictionary with product information and you want all active big images.  
```python
product = {
    "name": "really cool product",
    "images": {
        "active: {
            "small": [
                "https://www.smallimage.com",
                "https://www.smallimage.com",
                "https://www.smallimage.com",
            ],
            "big": [
                "https://www.bigimage.com",
                "https://www.bigimage.com",
                "https://www.bigimage.com",
            ]
        },
        "disabled": {
            "small": [
                "https://www.notcool.com",
                "https://www.notcool.com",
                "https://www.notcool.com",
            ],
            "big": [
                "https://www.notcool.com",
                "https://www.notcool.com",
                "https://www.notcool.com",
            ]
        }
    }
}
```

It's a simple one line function to get a value.  
```python
big_images = dget(product, "images", "active", "big", default=[])
```

Without the package you would have to do things like `try except`:  
```python
try:
    big_images = product["images"]["active"]["big"]
except:
    big_images = []
```

Or chain `get()` methods like:  
```python
big_images = product.get("images", {}).get("active", {}).get("big", [])
```

# usage
All that you need to know is that you will navigate like normally do with dictionaries or lists (using square brackets) but it will not raise exceptions if one field doesn't exist along the way.  
```python
list_ = [
    [1,2,3],
    [4,5,6],
    [7,8,9],
    [
        [10, 11, 12],
        [13, 14, 15],
        [16, 17, 18],
    ]
]

# Same as: list_[3][1][2]
value = dget(list_, 3, 1, 2)

print(value) # 15
```

```python
list_ = {
    "hello": {
        "annoing": {
            "dictionary": "here"
        }
    }
}

# Same as: list_["hello"]["annoing"]["dictionary"]
value = dget(list_, "hello", "annoing", "dictionary")

print(value) # "here"
```

It really doesn't care what strcuture it is.  
```python
list_ = {
    "first": {
        5: [
            "nice"
        ]
    }
}

# Same as: list_["first"][5][0]
value = dget(list_, "first", 5, 0)

print(value) # "nice"
```
