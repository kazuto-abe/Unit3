# Quiz20

### python code
```.py
class Swap():
    def __init__ (self, x:str):
        self.x = x

    def swap_characters(x):
        length = len(x)
        new_x = ""
        for i in range(0, length, 2):
            new_x = new_x + x[i+1] + x[i]

        print (new_x)
    
print(Swap.swap_characters(x = "01ABxy"))
```

### test result

![Screen Shot 2021-03-02 at 22 15 07](https://user-images.githubusercontent.com/60457723/109653829-cc74ed00-7ba4-11eb-9f06-e0824ba2ce45.png)
