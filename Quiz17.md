# Quiz17

Given three ints, a b c, one of them is small, one is medium and one is large. Return true if the three values are evenly spaced, so the difference between small and medium is the same as the difference between medium and large. 

evenlySpaced(2, 4, 6) → true <br>
evenlySpaced(4, 6, 2) → true <br>
evenlySpaced(4, 6, 3) → false <br>

### python code
```.py
class evaluation():
    def __init__(self, a, b, c):
        self.a:int = a
        self.b:int = b
        self.c:int = c

    def evenlySpaced(a,b,c):
        unsorted_nums = [a,b,c]
        sorted_nums = []
        length = len(unsorted_nums)
    
        for i in range (length):
            max = unsorted_nums[-1]
            for i in unsorted_nums:
                if i > max:
                    max = i
            sorted_nums.append(max)
            unsorted_nums.remove(max)
    
        if abs(sorted_nums[0] - sorted_nums[1]) == abs(sorted_nums[1] - sorted_nums[2]):
            return True
        else:
            return False

print(evaluation.evenlySpaced(a = 2,b = 4,c = 6))
print(evaluation.evenlySpaced(a = 4,b = 6,c = 2))
print(evaluation.evenlySpaced(a = 4,b = 6,c = 3))
```

### test result

![Screen Shot 2021-03-02 at 20 19 15](https://user-images.githubusercontent.com/60457723/109641058-9c255280-7b94-11eb-88c8-0473510eff65.png)

