# Python Programming Exercises - 120 Questions

## 1. Hello World
**Question:** Write a program that prints "Hello, World!" to the console.  
**Explanation:** This is the traditional first program. Simply output the exact string.  
**Input:** None  
**Output:** Hello, World!  
**Answer:** Hello, World!

```python
from sympy.printing.cxx import reserved
from mako.testing.helpers import result_lines
from pandas.core.computation.expr import intersection
from prometheus_client.decorator import append
from sqlalchemy.testing import startswith_
from sympy import print_tree

print("Hello, World!")
```

## 2. Basic Addition
**Question:** Add two numbers and print the result.  
**Explanation:** Take two integer values and calculate their sum.  
**Input:** a = 5, b = 3  
**Output:** Sum of the two numbers  
**Answer:** 8

```python
a = 5
b = 3
print("The sum is:", a + b)
```

## 3. Variable Assignment
**Question:** Create variables for your name and age, then print them.  
**Explanation:** Demonstrate basic variable assignment with string and integer types.  
**Input:** name = "Alice", age = 25  
**Output:** Print name and age  
**Answer:** Alice 25

```python
name = "Alice"
age = 25
print(f"my name is {name} and I am {age} years old.")
```

## 4. String Concatenation
**Question:** Combine two strings with a space between them.  
**Explanation:** Join two separate strings into one with proper spacing.  
**Input:** "Hello" and "World"  
**Output:** Combined string  
**Answer:** Hello World

```python
combined_string = "Hello" + " " + "World"
print(combined_string)
```

## 5. Integer Division
**Question:** Perform integer division of 17 by 3.  
**Explanation:** Use the floor division operator to get the quotient without remainder.  
**Input:** 17, 3  
**Output:** Integer quotient  
**Answer:** 5

```python
a = 17
b = 3
print("The integer division of", a, "by", b, "is:", a // b)
```

## 6. Modulo Operation
**Question:** Find the remainder when 17 is divided by 3.  
**Explanation:** Use the modulo operator to get the remainder of division.  
**Input:** 17, 3  
**Output:** Remainder  
**Answer:** 2

```python
a = 17
b = 3
print("The remainder when", a, "is divided by", b, "is:", a % b)
```

## 7. Boolean Comparison
**Question:** Check if 10 is greater than 5.  
**Explanation:** Use comparison operators to return a boolean value.  
**Input:** 10, 5  
**Output:** Boolean result  
**Answer:** True

```python
a = 10
b = 5
print(a > b)
```

## 8. String Length
**Question:** Find the length of the string "Python".  
**Explanation:** Use the built-in len() function to count characters.  
**Input:** "Python"  
**Output:** Number of characters  
**Answer:** 6

```python
a = "Python"
print(len(a))
```

## 9. List Creation
**Question:** Create a list with numbers 1, 2, 3, 4, 5.  
**Explanation:** Initialize a list with the specified integer values.  
**Input:** Numbers 1 through 5  
**Output:** List containing these numbers  
**Answer:** [1, 2, 3, 4, 5]

```python
a = [1, 2, 3, 4, 5]
print(a)
```

## 10. List Indexing
**Question:** Get the first and last element from the list [10, 20, 30, 40, 50].  
**Explanation:** Access elements using positive and negative indexing.  
**Input:** [10, 20, 30, 40, 50]  
**Output:** First and last elements  
**Answer:** 10, 50

```python
a = [10, 20, 30, 40, 50]
print("First element:", a[0])
print("Last element:", a[-1])
```

## 11. String Uppercase
**Question:** Convert the string "hello" to uppercase.  
**Explanation:** Use string method to transform all characters to uppercase.  
**Input:** "hello"  
**Output:** Uppercase string  
**Answer:** HELLO

```python
a = "hello"
print(a.upper())
print(a)  # Original string remains unchanged
```

## 12. Type Checking
**Question:** Check the type of the variable x = 42.  
**Explanation:** Use the type() function to determine the data type.  
**Input:** x = 42  
**Output:** Type of the variable  
**Answer:** <class 'int'>

```python
x = 42
print(type(x))
```

## 13. Float Conversion
**Question:** Convert the string "3.14" to a float.  
**Explanation:** Use type casting to convert string representation to floating-point number.  
**Input:** "3.14"  
**Output:** Float value  
**Answer:** 3.14

```python
a = "3.14"
print(float(a))
print(a)  # Original string remains unchanged
```

## 14. List Append
**Question:** Add the number 6 to the list [1, 2, 3, 4, 5].  
**Explanation:** Use the append method to add an element to the end of a list.  
**Input:** [1, 2, 3, 4, 5], append 6  
**Output:** Modified list  
**Answer:** [1, 2, 3, 4, 5, 6]

```python
a = [1, 2, 3, 4, 5]
a.append(6)
print(a)  # Output the modified list
for _ in range(6,12):
    a.append(_)
print(a)  # Output the modified list
```

## 15. Dictionary Creation
**Question:** Create a dictionary with keys 'name' and 'age' with values 'John' and 30.  
**Explanation:** Initialize a dictionary with string keys and mixed value types.  
**Input:** name: John, age: 30  
**Output:** Dictionary  
**Answer:** {'name': 'John', 'age': 30}

```python
data = []
values = int(input("Enter the number of entries: "))
end_value = int(input("Enter the end value: "))
for i in range(values, end_value):
    name = input("Enter your name: ")
    age = int(input("Enter your age: "))

    person = {'name': name, 'age': age}
    data.append(person)
print(data)
```

## 16. Dictionary Access
**Question:** Get the value of 'name' from the dictionary {'name': 'Alice', 'age': 25}.  
**Explanation:** Access dictionary values using key lookup.  
**Input:** {'name': 'Alice', 'age': 25}  
**Output:** Value of 'name' key  
**Answer:** Alice

```python
data = []
values = int(input("Enter the number of entries: "))
end_value = int(input("Enter the end value: "))
for i in range(values, end_value):
    name = input("Enter your name: ")
    age = int(input("Enter your age: "))

    person = {'name': name, 'age': age}
    data.append(person)
for entry in data:
    print(entry.get('name', None))  # Safely get the 'name' value from each dictionary in the list
    print(entry.get('age', None))

print(data)  # Output the entire list of dictionaries
```

## 17. Range Function
**Question:** Create a list of numbers from 1 to 5 using range().  
**Explanation:** Use range() function and convert to list to generate sequence.  
**Input:** Range from 1 to 6 (exclusive)  
**Output:** List of numbers  
**Answer:** [1, 2, 3, 4, 5]

```python
number = list(range(1, 6))
print(number)
```

## 18. String Slicing
**Question:** Get the first three characters of "Python".  
**Explanation:** Use string slicing with start and end indices.  
**Input:** "Python"  
**Output:** First three characters  
**Answer:** Pyt

```python
strings = "Python"
print(strings[:3])
```

## 19. List Slicing
**Question:** Get the middle three elements from [1, 2, 3, 4, 5, 6, 7].  
**Explanation:** Use list slicing to extract a subset of elements.  
**Input:** [1, 2, 3, 4, 5, 6, 7]  
**Output:** Middle three elements  
**Answer:** [3, 4, 5]

```python
list_numbers = [1, 2, 3, 4, 5, 6, 7]
print(list_numbers[2:5])
print(list_numbers)
```

## 20. String Replace
**Question:** Replace 'world' with 'Python' in "Hello world".  
**Explanation:** Use string replace method to substitute text.  
**Input:** "Hello world"  
**Output:** Modified string  
**Answer:** Hello Python

```python
strings = "Hello world"
modified_string = strings.replace("world", "Python")
print(modified_string)
print(strings)  # Original string remains unchanged
```

## 21. List Sum
**Question:** Calculate the sum of all numbers in [1, 2, 3, 4, 5].  
**Explanation:** Use the built-in sum() function on a list of numbers.  
**Input:** [1, 2, 3, 4, 5]  
**Output:** Sum of all elements  
**Answer:** 15

```python
number_list = [1, 2, 3, 4, "hello world"]
for i in number_list:
    if not isinstance(i, int):
        number_list.remove(i)
print(sum(number_list))
print(number_list)  # Original list remains unchanged
```

## 22. String Split
**Question:** Split the string "apple,banana,cherry" by comma.  
**Explanation:** Use string split method to create a list from delimited string.  
**Input:** "apple,banana,cherry"  
**Output:** List of fruits  
**Answer:** ['apple', 'banana', 'cherry']

```python
string_name = "apple,banana,cherry"
fruits = string_name.split(",")
print(fruits)
print(string_name)  # Original string remains unchanged
```

## 23. List Maximum
**Question:** Find the maximum value in [10, 5, 8, 20, 3].  
**Explanation:** Use the built-in without using max() function to find the largest element.  
**Input:** [10, 5, 8, 20, 3]  
**Output:** Maximum value  
**Answer:** 20

```python
number_list = [10, 5, 8, 20, 3]

for i in number_list:
    if not isinstance(i, int):
        number_list.remove(i)

max_number = number_list[0]
min_number = number_list[0]
for j in number_list:
    if max_number < j:
        max_number= j
    if min_number > j:
        min_number= j

print(max_number, "get the maximum number !")
print(min_number, "get the Minimum number !")
```

## 24. String Contains
**Question:** Check if "Python" contains the substring "hon".  
**Explanation:** Use the 'in' operator to test substring membership.  
**Input:** "Python", substring "hon"  
**Output:** Boolean result  
**Answer:** True

```python
main_string = "Python"
substring = "hon"

# Check if substring exists in string
result = substring in main_string

print("Substring exists:", result)
```

## 25. List Count
**Question:** Count how many times 3 appears in [1, 3, 3, 4, 3, 5].  
**Explanation:** Use the count method to find occurrences of a specific value.  
**Input:** [1, 3, 3, 4, 3, 5]  
**Output:** Count of occurrences  
**Answer:** 3

```python
number_list = [1,3,3,4,3,5, "student"]
for i in number_list:
    if not isinstance(i, int):
        number_list.remove(i)
count_number = {}
for num in number_list:
    if num in count_number:
        count_number[num] +=1
    else:
        count_number[num] = 1
print(count_number)

string_name = "nandkishore"
count_string = {}
for i in string_name:
    if i in count_string:
        count_string[i] += 1
    else:
        count_string[i] = 1
    print(i)

print(count_string, "count String !!")
```

## 26. String Reverse
**Question:** Reverse the string "hello".  
**Explanation:** Use string slicing with step -1 to reverse character order.  
**Input:** "hello"  
**Output:** Reversed string  
**Answer:** olleh

```python
string_ = "hello"
reserved_string = ""
for i in string_:
    reserved_string = i + reserved_string

    print(reserved_string)
print(reserved_string)

print(string_[::-1])
```

## 27. List Reverse
**Question:** Reverse the list [1, 2, 3, 4, 5].  
**Explanation:** Use slicing or reverse method to change element order.  
**Input:** [1, 2, 3, 4, 5]  
**Output:** Reversed list  
**Answer:** [5, 4, 3, 2, 1]

```python
num_list = [1,2,3,4,5]
reverse_list = []
for num in num_list:
    reverse_list = [num] + reverse_list

    print(num)

print(reverse_list)
```

## 28. Tuple Creation
**Question:** Create a tuple with elements 1, 2, 3.  
**Explanation:** Initialize an immutable sequence with the given values.  
**Input:** Elements 1, 2, 3  
**Output:** Tuple  
**Answer:** (1, 2, 3)

```python
num_tuple = (1,2,3,4,5,5)
print(num_tuple)
print(type(num_tuple))
```

## 29. Set Creation
**Question:** Create a set from the list [1, 2, 2, 3, 3, 4].  
**Explanation:** Convert list to set to remove duplicates.  
**Input:** [1, 2, 2, 3, 3, 4]  
**Output:** Set with unique elements  
**Answer:** {1, 2, 3, 4}

```python
num_list = [1, 2, 2, 3, 3, 4]
num_set = set(num_list)
print(num_set)
print(type(num_set))
```

## 30. Dictionary Keys
**Question:** Get all keys from {'a': 1, 'b': 2, 'c': 3}.  
**Explanation:** Use the keys() method to extract dictionary keys.  
**Input:** {'a': 1, 'b': 2, 'c': 3}  
**Output:** Dictionary keys  
**Answer:** dict_keys(['a', 'b', 'c'])

```python
dict_value = {'a': 1, 'b': 2, 'c': 3}
get_key = dict_value.keys()
get_item = dict_value.items()
new_dict = {}

for key, value in get_item:
    new_dict[f"{value}{key}"] =f"{key}"

print(new_dict)
```

## 31. String Lowercase
**Question:** Convert "HELLO" to lowercase.  
**Explanation:** Use string method to transform all characters to lowercase.  
**Input:** "HELLO"  
**Output:** Lowercase string  
**Answer:** hello

```python
string_var = "HELLO"
lower_case = string_var.lower()
print(lower_case)
```

## 32. List Insert
**Question:** Insert 99 at index 2 in the list [1, 2, 3, 4, 5].  
**Explanation:** Use insert method to add element at specific position.  
**Input:** [1, 2, 3, 4, 5], insert 99 at index 2  
**Output:** Modified list  
**Answer:** [1, 2, 99, 3, 4, 5]

```python
num_list = [1, 2, 3, 4, 5]
new_list = []
insert_value = int(input("Enter the Values for insert in list: "))
insert_no = int(input("Enter the insert place no. : "))
for j, i in enumerate(num_list):
    if j == insert_no:
        print(insert_value, "insert values ")

        new_list.append(insert_value)
    else:
        new_list.append(i)

print(new_list, "get new list")
    print(j)
    print(i)
    new_list.append()
```

## 33. String Join
**Question:** Join the list ['a', 'b', 'c'] with '-' as separator.  
**Explanation:** Use string join method to combine list elements.  
**Input:** ['a', 'b', 'c']  
**Output:** Joined string  
**Answer:** a-b-c

```python
string_var = ['a', 'b', 'c']
new_string = '-'.join(string_var)
print(new_string)

string_var = ['a', 'b', 'c']
new_string = ''

for i in string_var:
    if new_string:
        new_string += '-'
    new_string += i
print(new_string)
```

## 34. Absolute Value
**Question:** Find the absolute value of -15.  
**Explanation:** Use the abs() function to get non-negative value.  
**Input:** -15  
**Output:** Absolute value  
**Answer:** 15

```python
print(abs(-15))
```

## 35. Power Operation
**Question:** Calculate 2 to the power of 8.  
**Explanation:** Use the ** operator or pow() function for exponentiation.  
**Input:** base = 2, exponent = 8  
**Output:** Result of exponentiation  
**Answer:** 256

```python
print(2**8)
print(pow(2, 8))
actual_num = int(input("Enter the Number. :"))
pow_num = int(input("Enter the Pow Number. :"))
```

## 36. Round Function
**Question:** Round 3.7 to the nearest integer.  
**Explanation:** Use the round() function for rounding to nearest whole number.  
**Input:** 3.7  
**Output:** Rounded integer  
**Answer:** 4

```python
print(round(3.7))
```

## 37. String Strip
**Question:** Remove whitespace from " hello ".  
**Explanation:** Use strip method to remove leading and trailing whitespace.  
**Input:** "  hello  "  
**Output:** Stripped string  
**Answer:** hello

```python
string_var = " hello "
string_var.split()
print(string_var)
```

## 38. List Remove
**Question:** Remove the first occurrence of 3 from [1, 3, 2, 3, 4].  
**Explanation:** Use remove method to delete the first matching element.  
**Input:** [1, 3, 2, 3, 4]  
**Output:** List after removal  
**Answer:** [1, 2, 3, 4]

```python
num_list = [1, 3, 2, 3, 4]
remove_index = 1
new_list = []

for j, i in enumerate(num_list):
    if j ==remove_index:
        pass
    else:
        new_list.append(i)
    print(i)
print(new_list)
```

## 39. Dictionary Values
**Question:** Get all values from {'x': 10, 'y': 20, 'z': 30}.  
**Explanation:** Use the values() method to extract dictionary values.  
**Input:** {'x': 10, 'y': 20, 'z': 30}  
**Output:** Dictionary values  
**Answer:** dict_values([10, 20, 30])

```python
dict_value = {'x': 10, 'y': 20, 'z': 30}
print(dict_value.values())
```

## 40. String Find
**Question:** Find the index of 'o' in "hello".  
**Explanation:** Use find method to locate substring position.  
**Input:** "hello", search for 'o'  
**Output:** Index of character  
**Answer:** 4

```python
sting_var = "hello"
search_var = "o"
for j, i in enumerate(sting_var):
    if i is search_var:
        print(j)
    print(i)
```

## 41. List Pop
**Question:** Remove and return the last element from [1, 2, 3, 4, 5].  
**Explanation:** Use pop method to remove and return the last element.  
**Input:** [1, 2, 3, 4, 5]  
**Output:** Removed element and modified list  
**Answer:** 5, [1, 2, 3, 4]

```python
num_list = [1,2,3,4,5,8,9]
num_len = (len(num_list)-1)
new_list = []
for j, i in enumerate(num_list):
    if j==num_len:
        pass
    else:
        new_list.append(i)
    print(i)
print(new_list)
```

## 42. String Count
**Question:** Count occurrences of 'l' in "hello".  
**Explanation:** Use count method to find how many times a character appears.  
**Input:** "hello", count 'l'  
**Output:** Number of occurrences  
**Answer:** 2

```python
string_var = "hello"
# print(string_var.count("l"))
string_count={}
for j, i in enumerate(string_var):
    if i in string_count:
        string_count[i] += 1
    else:
        string_count[i] = 1


print(string_count)
```

## 43. List Extend
**Question:** Extend [1, 2, 3] with [4, 5, 6].  
**Explanation:** Use extend method to add multiple elements from another iterable.  
**Input:** [1, 2, 3], extend with [4, 5, 6]  
**Output:** Extended list  
**Answer:** [1, 2, 3, 4, 5, 6]

```python
list1 = [1,2,3]
list2 = [4,5,6]
list_num = list1 + list2
print(list_num)
```

## 44. Dictionary Update
**Question:** Update {'a': 1} with {'b': 2, 'c': 3}.  
**Explanation:** Use update method to merge dictionaries.  
**Input:** {'a': 1}, update with {'b': 2, 'c': 3}  
**Output:** Updated dictionary  
**Answer:** {'a': 1, 'b': 2, 'c': 3}

```python
dict_value = {'a': 1}
dict_value.update({'b': 2, 'c': 3})
print(dict_value)
```

## 45. Set Union
**Question:** Find the union of sets {1, 2, 3} and {3, 4, 5}.  
**Explanation:** Combine two sets to get all unique elements.  
**Input:** {1, 2, 3} and {3, 4, 5}  
**Output:** Union set  
**Answer:** {1, 2, 3, 4, 5}

```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}
set_union = set1.union(set2)
set_interception = set1.intersection(set2)
print(set_union, "set_union")
print(set_interception, "set_interception")
```

## 46. String Startswith
**Question:** Check if "Python" starts with "Py".  
**Explanation:** Use startswith method to test string prefix.  
**Input:** "Python", prefix "Py"  
**Output:** Boolean result  
**Answer:** True

```python
string_var = "Python"
print(string_var.startswith("Py"))
```

## 47. List Clear
**Question:** Clear all elements from [1, 2, 3, 4, 5].  
**Explanation:** Use clear method to remove all elements from list.  
**Input:** [1, 2, 3, 4, 5]  
**Output:** Empty list  
**Answer:** []

```python
list_var = [1,2,3,4,5]
list_var.clear()
print(list_var)
```

## 48. String Endswith
**Question:** Check if "filename.txt" ends with ".txt".  
**Explanation:** Use endswith method to test string suffix.  
**Input:** "filename.txt", suffix ".txt"  
**Output:** Boolean result  
**Answer:** True

```python
file_name = "filename.txt"
print(file_name.endswith(".txt"))
```

## 49. Tuple Indexing
**Question:** Get the second element from (10, 20, 30, 40).  
**Explanation:** Access tuple elements using index notation.  
**Input:** (10, 20, 30, 40)  
**Output:** Second element  
**Answer:** 20

```python
tuple_var = (10,20,30,40)
get_value=tuple_var[1]
print(get_value)
```

## 50. Set Intersection
**Question:** Find common elements between {1, 2, 3, 4} and {3, 4, 5, 6}.  
**Explanation:** Use intersection to find elements present in both sets.  
**Input:** {1, 2, 3, 4} and {3, 4, 5, 6}  
**Output:** Intersection set  
**Answer:** {3, 4}

```python
set1 ={1, 2, 3, 4}
set2 = {3, 4, 5, 6}
intersection_data = set1.intersection(set2)
print(intersection_data)
```

## 51. String Title
**Question:** Convert "hello world" to title case.  
**Explanation:** Use title method to capitalize first letter of each word.  
**Input:** "hello world"  
**Output:** Title case string  
**Answer:** Hello World

```python
string_var = "hello world"
string_var = string_var.capitalize()
print(string_var)
```

## 52. List Index
**Question:** Find the index of 'banana' in ['apple', 'banana', 'cherry'].  
**Explanation:** Use index method to locate element position.  
**Input:** ['apple', 'banana', 'cherry']  
**Output:** Index of 'banana'  
**Answer:** 1

```python
str_list = ['apple', 'banana', 'cherry']
index_value = str_list.index("banana")
print(index_value)
print(str_list)
```

## 53. Dictionary Get
**Question:** Get the value of 'age' from {'name': 'John', 'city': 'NYC'} with default 0.  
**Explanation:** Use get method with default value for safe key access.  
**Input:** {'name': 'John', 'city': 'NYC'}, key 'age', default 0  
**Output:** Value or default  
**Answer:** 0

```python
dict_str = {'name': 'John', 'city': 'NYC'}
print(dict_str)
age = dict_str.get("age", 0)
print(age)
```

## 54. Set Difference
**Question:** Find elements in {1, 2, 3, 4} that are not in {3, 4, 5}.  
**Explanation:** Use set difference to find unique elements in first set.  
**Input:** {1, 2, 3, 4} and {3, 4, 5}  
**Output:** Difference set  
**Answer:** {1, 2}

```python
set_var1 = {1,2,3,4}
set_var2 = {3,4,5}
difference_set = set_var1.difference(set_var2)
print(difference_set)
```

## 55. String Replace All
**Question:** Replace all 'a' with 'e' in "banana".  
**Explanation:** Use replace method to substitute all occurrences.  
**Input:** "banana", replace 'a' with 'e'  
**Output:** Modified string  
**Answer:** benene

```python
string_var ="Banana"
replace_str = string_var.replace("a", "e")
print(replace_str)
```

## 56. List Copy
**Question:** Create a copy of [1, 2, 3].  
**Explanation:** Use copy method or slicing to create independent list copy.  
**Input:** [1, 2, 3]  
**Output:** Copied list  
**Answer:** [1, 2, 3]

```python
list_var = [1,2,3]
copy_var = list_var.copy()
print(copy_var)
```

## 57. Tuple Length
**Question:** Find the length of (1, 2, 3, 4, 5, 6).  
**Explanation:** Use len() function to count tuple elements.  
**Input:** (1, 2, 3, 4, 5, 6)  
**Output:** Tuple length  
**Answer:** 6

```python
tuple_var = (1,2,3,4,5,6)
tuple_length= len(tuple_var)
print(tuple_length)
```

## 58. String Isdigit
**Question:** Check if "123" contains only digits.  
**Explanation:** Use isdigit method to verify numeric characters.  
**Input:** "123"  
**Output:** Boolean result  
**Answer:** True

```python
check_digit = "123"
check = check_digit.isdigit()
print(check)
```

## 59. Set Add
**Question:** Add 4 to the set {1, 2, 3}.  
**Explanation:** Use add method to insert new element into set.  
**Input:** {1, 2, 3}, add 4  
**Output:** Modified set  
**Answer:** {1, 2, 3, 4}

```python
set_var = {1,2,3}
set_var.add(4)
print(set_var)
```

## 60. String Swapcase
**Question:** Swap the case of "Hello World".  
**Explanation:** Use swapcase method to toggle upper/lowercase characters.  
**Input:** "Hello World"  
**Output:** Case-swapped string  
**Answer:** hELLO wORLD

```python
string_var = "Hello World"
string_swapcase = string_var.swapcase()
print(string_swapcase)
```

## 61. List Sort
**Question:** Sort the list [3, 1, 4, 1, 5, 9] in ascending order.  
**Explanation:** Use sort method to arrange elements in order.  
**Input:** [3, 1, 4, 1, 5, 9]  
**Output:** Sorted list  
**Answer:** [1, 1, 3, 4, 5, 9]

```python
list_var = [3, 1, 4, 1, 5, 9]
sort_list = sorted(list_var)
print(sort_list)

list_var = [3, 1, 4, 1, 5, 9]
n = len(list_var)
for i in range(n):
    print(i, "print i")
    for j in range(0, n-i-1):
        print(j, "print j")
        if list_var[j] > list_var[j+1]:
            print(list_var, "print list var")

            temp = list_var[j]
            list_var[j] = list_var[j+1]
            list_var[j+1] = temp

print(list_var)    # break

list_var = [3,1,4,1,5,9]
n = len(list_var)
for i in range(n):
    for j in range(0, n-i-1):
        if list_var[j] > list_var[j+1]:
            temp = list_var[j]
            list_var[j] = list_var[j+1]
            list_var[j+1] = temp

print(list_var)
```

## 62. Dictionary Pop
**Question:** Remove and return the value of 'b' from {'a': 1, 'b': 2, 'c': 3}.  
**Explanation:** Use pop method to remove key-value pair and return value.  
**Input:** {'a': 1, 'b': 2, 'c': 3}, pop key 'b'  
**Output:** Popped value and modified dict  
**Answer:** 2, {'a': 1, 'c': 3}

```python
dict_var = {'a': 1, 'b': 2, 'c': 3}
dict_var.pop("b")
print(dict_var)
```

## 63. String Center
**Question:** Center "hi" in a field of width 10 using '*' as fill character.  
**Explanation:** Use center method to pad string symmetrically.  
**Input:** "hi", width 10, fillchar '*'  
**Output:** Centered string  
**Answer:** ****hi****

```python
staring_var = "hi"
centered = staring_var.center(10, "*")
print(centered)

string_var = "hi"
width = 10
fillchar = "*"

total_padding = width - len(string_var)
left_padding = total_padding//2
right_padding = total_padding-left_padding
certercide = f"{left_padding*fillchar}{string_var}{right_padding*fillchar}"
print(certercide)
```

## 64. List Minimum
**Question:** Find the minimum value in [10, 5, 8, 20, 3].  
**Explanation:** Use the built-in min() function to find smallest element.  
**Input:** [10, 5, 8, 20, 3]  
**Output:** Minimum value  
**Answer:** 3

```python
num_list = [10,5,8,20,3]
get_min = min(num_list)
print(get_min)

num_list = [10,5,8,20,3]
n = len(num_list)
for i in range(n):
    for j in range(0, n-i-1):
        if num_list[j] > num_list[j+1]:
            temp = num_list[j]
            num_list[j] = num_list[j+1]
            num_list[j+1] = temp
print(num_list[0])
```

## 65. Set Remove
**Question:** Remove 2 from the set {1, 2, 3, 4}.  
**Explanation:** Use remove method to delete specific element from set.  
**Input:** {1, 2, 3, 4}, remove 2  
**Output:** Modified set  
**Answer:** {1, 3, 4}

```python
set_var = {1,2,3,4}
set_var.remove(2)
print(set_var)
```

## 66. String Ljust
**Question:** Left-justify "hi" in a field of width 8 using '-'.  
**Explanation:** Use ljust method to pad string on the right.  
**Input:** "hi", width 8, fillchar '-'  
**Output:** Left-justified string  
**Answer:** hi------

```python
staring_var = "hi"
width=8
fillchar = "-"
new_str = staring_var.ljust(9, fillchar)
print(new_str)

string_var = "hi"
width = 8
fillchar = "-"
new_str = f"{string_var}"+f"{width*fillchar}"
print(new_str)
```

## 67. Tuple Count
**Question:** Count occurrences of 2 in (1, 2, 2, 3, 2).  
**Explanation:** Use count method to find how many times value appears.  
**Input:** (1, 2, 2, 3, 2), count 2  
**Output:** Number of occurrences  
**Answer:** 3

```python
tuple_var = (1,2,2,3,2)
count_var = tuple_var.count(2)
print(count_var)

tuple_var = (1,2,2,3,2)
duplicate_var = {}
for i in tuple_var:
    if i in duplicate_var:
        duplicate_var[i] +=1
    else:
        duplicate_var[i] = 1
print(duplicate_var.get(2))
```

## 68. String Isalpha
**Question:** Check if "hello" contains only alphabetic characters.  
**Explanation:** Use isalpha method to verify alphabetic content.  
**Input:** "hello"  
**Output:** Boolean result  
**Answer:** True

```python
string_var = "hello"
check_char = string_var.isalpha()
print(check_char)
```

## 69. List Insert Multiple
**Question:** Insert [10, 20] at index 1 in [1, 2, 3].  
**Explanation:** Use slicing assignment to insert multiple elements.  
**Input:** [1, 2, 3], insert [10, 20] at index 1  
**Output:** Modified list  
**Answer:** [1, 10, 20, 2, 3]

```python
num_list1 = [10,20]
num_list2 = [1,2,3]

new_num = num_list1[:1] + num_list2 + num_list1[1:]
print(new_num)
```

## 70. Dictionary Items
**Question:** Get all key-value pairs from {'x': 1, 'y': 2}.  
**Explanation:** Use items method to get tuples of key-value pairs.  
**Input:** {'x': 1, 'y': 2}  
**Output:** Dictionary items  
**Answer:** dict_items([('x', 1), ('y', 2)])

```python
dict_var = {'x': 1, 'y': 2}
dict_item = dict_var.items()
print(dict_item)
```

## 71. String Zfill
**Question:** Pad "42" with zeros to make it 5 characters long.  
**Explanation:** Use zfill method to pad numeric string with leading zeros.  
**Input:** "42", width 5  
**Output:** Zero-padded string  
**Answer:** 00042

```python
str_var = "42"
new_var = str_var.zfill(5)
print(new_var)
```

## 72. Set Discard
**Question:** Safely remove 5 from {1, 2, 3} without raising error if not present.  
**Explanation:** Use discard method which doesn't raise KeyError.  
**Input:** {1, 2, 3}, discard 5  
**Output:** Unchanged set  
**Answer:** {1, 2, 3}

```python
set_var = {1,2,3}
# set_var.discard(5)
set_var.remove(5)
print(set_var)
```

## 73. List Multiplication
**Question:** Create a list with "hello" repeated 3 times.  
**Explanation:** Use list multiplication operator to repeat elements.  
**Input:** "hello", repeat 3 times  
**Output:** List with repeated elements  
**Answer:** ['hello', 'hello', 'hello']

```python
str_var = "hello"
multiple_list = [str_var]*3
print(multiple_list)
```

## 74. String Partition
**Question:** Partition "hello-world" at the first '-'.  
**Explanation:** Use partition method to split string into three parts.  
**Input:** "hello-world", separator '-'  
**Output:** Tuple of three parts  
**Answer:** ('hello', '-', 'world')

```python
str_var = "hello-world"
new_str = str_var.partition("-")
print(new_str)

str_var = "hello-world"
separator = "-"
index = -1

for i in range(len(str_var)):
    if str_var[i] == separator:
        index = i
        break

if index != -1:
    before = str_var[:index]
    sep = separator
    after = str_var[index+1:]
    result = (before, sep, after)
else:
    result = (str_var, "", "")

print(result)
```

## 75. Enumerate Basic
**Question:** Get index-value pairs for ['a', 'b', 'c'].  
**Explanation:** Use enumerate to get (index, value) tuples.  
**Input:** ['a', 'b', 'c']  
**Output:** Enumerated pairs  
**Answer:** [(0, 'a'), (1, 'b'), (2, 'c')]

```python
str_list = ['a', 'b', 'c']
result = list(enumerate(str_list))
print(result)
```

## 76. Simple If-Else
**Question:** Check if a number is positive, negative, or zero.  
**Explanation:** Use conditional statements to categorize the input number.  
**Input:** number = -5  
**Output:** Category string  
**Answer:** negative

```python
number = int(input("Enter the value:"))
if number > 0:
    print("Positive")
if number < 0:
    print("Negative")
else:
    print("0")
```

## 77. For Loop Sum
**Question:** Calculate sum of numbers from 1 to 10 using a for loop.  
**Explanation:** Iterate through range and accumulate the sum.  
**Input:** Range 1 to 10 (inclusive)  
**Output:** Sum  
**Answer:** 55

```python
num_list=[]
for i in range(0,11):
    num_list.append(i)
print(num_list)
print(sum(num_list))
```

## 78. While Loop Countdown
**Question:** Print numbers from 5 down to 1 using while loop.  
**Explanation:** Use while loop with decrementing counter.  
**Input:** Start from 5  
**Output:** Numbers in descending order  
**Answer:** 5 4 3 2 1

```python
number = int(input("Enter the no for sum:"))

while number >=1:
    print(number)
    number -= 1
```

## 79. List Comprehension Basic
**Question:** Create a list of squares for numbers 1 to 5.  
**Explanation:** Use list comprehension to generate squared values.  
**Input:** Numbers 1 to 5  
**Output:** List of squares  
**Answer:** [1, 4, 9, 16, 25]

```python
number = int(input("Enter the Number:"))
list_comprehension = [x**2 for x in range(number)]
list_comprehension = [x**x for x in range(1,number)]
print(list_comprehension)
```

## 80. Function Definition
**Question:** Define a function that returns the square of a number.  
**Explanation:** Create a function that takes one parameter and returns its square.  
**Input:** Function call with 4  
**Output:** Squared value  
**Answer:** 16

```python
def numbers(num, var):
    power_num = num**var
    return power_num
number = int(input("Enter the Num no.:"))
power = int(input("Enter the power no.:"))
print(numbers(number, power))
```

## 81. Multiple Return Values
**Question:** Create a function that returns both quotient and remainder of division.  
**Explanation:** Return multiple values as a tuple from division operation.  
**Input:** 17, 3  
**Output:** Quotient and remainder  
**Answer:** (5, 2)

```python
def numbers(num, var):
    division = num//var
    modules = num%var
    return f"Division Value:{division} and Reminder is: {modules}"
number = int(input("Enter the Num no.:"))
power = int(input("Enter the power no.:"))

print(numbers(number, power))
```

## 82. Default Parameters
**Question:** Create a function with default parameter value.  
**Explanation:** Define function where second parameter defaults to 1.  
**Input:** Function call with one argument 5  
**Output:** Result using default  
**Answer:** 5 (if function multiplies by default 1)

```python
def factorial(num, multiple=1):
    num_multiple = num * multiple
    return num_multiple
print(factorial(5))
```

## 83. Lambda Function
**Question:** Create a lambda function to multiply two numbers.  
**Explanation:** Define anonymous function for multiplication operation.  
**Input:** 3, 4  
**Output:** Product  
**Answer:** 12

```python
number = int(input("Enter the Num no.:"))
power = int(input("Enter the power no.:"))
square_var = lambda number, power :number**power
print(square_var(number, power))
```

## 84. Filter Function
**Question:** Filter even numbers from [1, 2, 3, 4, 5, 6, 7, 8].  
**Explanation:** Use filter with lambda to select even numbers only.  
**Input:** [1, 2, 3, 4, 5, 6, 7, 8]  
**Output:** Even numbers  
**Answer:** [2, 4, 6, 8]

```python
num_filter = [1, 2, 3, 4, 5, 6, 7, 8]
even_lambda = lambda num: [x for x in num_filter if x%2==0]
print(even_lambda(num_filter))

num_filter = [1, 2, 3, 4, 5, 6, 7, 8]
even_lambda = list(filter(lambda x : x % 2 == 0, num_filter))
print(even_lambda)
```

## 85. Map Function
**Question:** Double all numbers in [1, 2, 3, 4, 5] using map.  
**Explanation:** Apply doubling function to each element using map.  
**Input:** [1, 2, 3, 4, 5]  
**Output:** Doubled numbers  
**Answer:** [2, 4, 6, 8, 10]

```python
map_var = [1, 2, 3, 4, 5]
map_lambda = list(map(lambda x: x**2 , map_var))
print(map_lambda)
```

## 86. Exception Handling
**Question:** Handle division by zero error.  
**Explanation:** Use try-except to catch ZeroDivisionError and return safe value.  
**Input:** 10, 0  
**Output:** Safe result or error message  
**Answer:** Error: Cannot divide by zero

```python
def exception_handle(num, var):
    try:
        return num/var
    except ZeroDivisionError as e:
        return str(e)
print(exception_handle(10,0))
```

## 87. String Format
**Question:** Format "Hello, {name}! You are {age} years old." with name="Alice" and age=30.  
**Explanation:** Use string format method with named placeholders.  
**Input:** Template string, name="Alice", age=30  
**Output:** Formatted string  
**Answer:** Hello, Alice! You are 30 years old.

```python
name="Alice"
age = 30

variables = f"Hello, {name}! You are {age} years old."
print(variables)
```

## 88. List Comprehension with Condition
**Question:** Get even numbers from 1 to 10 using list comprehension.  
**Explanation:** Combine list comprehension with conditional filtering.  
**Input:** Range 1 to 10  
**Output:** Even numbers list  
**Answer:** [2, 4, 6, 8, 10]

```python
list_comprehension = [x for x in range(1, 10) if x%2==0]
print(list_comprehension)
```

## 89. Dictionary Comprehension
**Question:** Create dictionary mapping numbers 1-5 to their squares.  
**Explanation:** Use dictionary comprehension to generate key-value pairs.  
**Input:** Numbers 1 to 5  
**Output:** Number to square mapping  
**Answer:** {1: 1, 2: 4, 3: 9, 4: 16, 5: 25}

```python
dictionary_comprehension = {x: x**2 for x in range(1, 6)}
print(dictionary_comprehension)
```

## 90. Nested List Access
**Question:** Get the element at position [1][2] from [[1, 2], [3, 4, 5], [6, 7, 8, 9]].  
**Explanation:** Access elements in nested list structure using double indexing.  
**Input:** [[1, 2], [3, 4, 5], [6, 7, 8, 9]]  
**Output:** Element at [1][2]  
**Answer:** 5

```python
nested_list = [[1, 2], [3, 4, 5], [6, 7, 8, 9]]
print(nested_list[1][2])
```

## 91. String Formatting f-strings
**Question:** Use f-string to format "The result is {result}" where result=42.  
**Explanation:** Use f-string literal for variable interpolation.  
**Input:** result = 42  
**Output:** Formatted string  
**Answer:** The result is 42

```python
result = 42
result_var = f"The result is {result}"
print(result_var)
```

## 92. Zip Function
**Question:** Combine [1, 2, 3] and ['a', 'b', 'c'] using zip.  
**Explanation:** Pair corresponding elements from two iterables.  
**Input:** [1, 2, 3] and ['a', 'b', 'c']  
**Output:** Zipped pairs  
**Answer:** [(1, 'a'), (2, 'b'), (3, 'c')]

```python
num_list = [1,2,3]
char_list = ["a","b","c"]

item_list = []
for item in zip(num_list, char_list):
    item_list.append(item)
print(item_list)
```

## 93. Any Function
**Question:** Check if any element in [False, False, True, False] is True.  
**Explanation:** Use any() to test if at least one element is truthy.  
**Input:** [False, False, True, False]  
**Output:** Boolean result  
**Answer:** True

```python
values = [False, False, True, False]
result = any(values)
print(result)
```

## 94. All Function
**Question:** Check if all elements in [True, True, False, True] are True.  
**Explanation:** Use all() to test if every element is truthy.  
**Input:** [True, True, False, True]  
**Output:** Boolean result  
**Answer:** False

```python
values = [True, True, False, True]
result = all(values)
print(result)
```

## 95. Sorted Function
**Question:** Sort ['banana', 'apple', 'cherry'] alphabetically.  
**Explanation:** Use sorted() to create new sorted list without modifying original.  
**Input:** ['banana', 'apple', 'cherry']  
**Output:** Sorted list  
**Answer:** ['apple', 'banana', 'cherry']

```python
fruit_list = ['banana', 'apple', 'cherry']
new_list = sorted(fruit_list)
print(new_list)

fruit_list = ['banana', 'apple', 'cherry']
n = len(fruit_list)
for i in range(n):
    for j in range(0, n-i-1):
        if fruit_list[j] > fruit_list[j+1]:
            temp = fruit_list[j]
            fruit_list[j] = fruit_list[j+1]
            fruit_list[j+1] = temp
print(fruit_list)
```

## 96. Reversed Function
**Question:** Reverse [1, 2, 3, 4, 5] using reversed().  
**Explanation:** Use reversed() function to create reverse iterator.  
**Input:** [1, 2, 3, 4, 5]  
**Output:** Reversed sequence  
**Answer:** [5, 4, 3, 2, 1]

```python
num_list = [1, 2, 3, 4, 5]
n = len(num_list)
for i in range(n):
    for j in range(0, n-i-1):
        if num_list[j] < num_list[j+1]:
            temp = num_list[j]
            num_list[j] = num_list[j+1]
            num_list[j+1] = temp
print(num_list)

num_list = [1, 2, 3, 4, 5]
reverse_list = list(reversed(num_list))
print(reverse_list)
```

## 97. Set Comprehension
**Question:** Create set of squares for numbers 1-5 using set comprehension.  
**Explanation:** Generate unique squared values using set comprehension syntax.  
**Input:** Numbers 1 to 5  
**Output:** Set of squares  
**Answer:** {1, 4, 9, 16, 25}

```python
set1 = {x for x in range(1, 5)}
print(set1)
```

## 98. Nested Dictionary
**Question:** Access the value 'Python' from {'lang': {'name': 'Python', 'version': 3.9}}.  
**Explanation:** Navigate nested dictionary structure using chained key access.  
**Input:** {'lang': {'name': 'Python', 'version': 3.9}}  
**Output:** Value of nested key  
**Answer:** Python

```python
input_list = input("Enter the values :")
print(input_list)
```

## 99. List Slice Assignment
**Question:** Replace elements at indices 1-3 in [1, 2, 3, 4, 5] with [10, 20].  
**Explanation:** Use slice assignment to replace multiple elements.  
**Input:** [1, 2, 3, 4, 5], replace [1:4] with [10, 20]  
**Output:** Modified list  
**Answer:** [1, 10, 20, 5]

```python
num_list = [1, 2, 3, 4, 5]
num_list[1:4] = [10, 20]
print(num_list)
```

## 100. String Translate
**Question:** Remove all vowels from "hello world" using translate.  
**Explanation:** Use str.maketrans and translate to remove specific characters.  
**Input:** "hello world"  
**Output:** String without vowels  
**Answer:** hll wrld

```python
str_var = "hello world"
remove_vowels = str.maketrans('', '', 'aeiouAEIOU')
result = str_var.translate(remove_vowels)

print(result)

str_var = "hello world"
vowels = "aeiouAEIOU"
result = ""

for char in str_var:
    if char not in vowels:   # skip vowels
        result += char

print(result)
```

## 101. For Loop with Enumerate
**Question:** Print index and value for each item in ['a', 'b', 'c'].  
**Explanation:** Use enumerate in for loop to get both index and value.  
**Input:** ['a', 'b', 'c']  
**Output:** Index-value pairs  
**Answer:** 0: a, 1: b, 2: c

```python
char_list = ['a', 'b', 'c']

for i, j in enumerate(char_list):
    print(f"{i}:{j}")
```

## 102. Nested For Loops
**Question:** Print all combinations of [1, 2] and ['a', 'b'].  
**Explanation:** Use nested loops to generate all possible pairs.  
**Input:** [1, 2] and ['a', 'b']  
**Output:** All combinations  
**Answer:** (1, 'a'), (1, 'b'), (2, 'a'), (2, 'b')

```python
list1 = [1,2]
list2 = ["a","b"]
for i in list1:
    for j in list2:
        print((i,j))
```

## 103. Break Statement
**Question:** Find the first number greater than 5 in [1, 3, 7, 4, 9, 2].  
**Explanation:** Use for loop with break to stop at first match.  
**Input:** [1, 3, 7, 4, 9, 2]  
**Output:** First number > 5  
**Answer:** 7

```python
num_list =  [1, 3, 7, 4, 9, 2]
for i in num_list:
    if i >5:
        print(i)
        break
```

## 104. Continue Statement
**Question:** Print all odd numbers from 1 to 10 using continue.  
**Explanation:** Skip even numbers using continue in loop.  
**Input:** Range 1 to 10  
**Output:** Odd numbers only  
**Answer:** 1, 3, 5, 7, 9

```python
odd_list = []
for i in range(0,10):
    if i%2 !=0:
        print(i)
        odd_list.append(i)
print(odd_list)
```

## 105. Else with For Loop
**Question:** Check if 6 exists in [1, 2, 3, 4, 5] using for-else.  
**Explanation:** Use else clause with for loop to handle "not found" case.  
**Input:** [1, 2, 3, 4, 5], search for 6  
**Output:** Found or not found message  
**Answer:** 6 not found

```python
num_list = [1, 2, 3, 4, 5]
value = 6

for i in num_list:
    if i == value:
        print(f"{value} found")
        break
else:
    print(f"{value} not found")
```

## 106. Multiple Assignment
**Question:** Assign values 1, 2, 3 to variables a, b, c in one line.  
**Explanation:** Use tuple unpacking for multiple variable assignment.  
**Input:** Values 1, 2, 3  
**Output:** Variables a, b, c  
**Answer:** a=1, b=2, c=3

```python
a,b,c=1,2,3
print(a)
print(b)
print(c)
```

## 107. Swap Variables
**Question:** Swap the values of x=10 and y=20.  
**Explanation:** Use tuple unpacking to exchange variable values.  
**Input:** x=10, y=20  
**Output:** Swapped values  
**Answer:** x=20, y=10

```python
x=10
y =20
x, y = y, x
print("x =", x)
print("y =", y)
```

## 108. Variable Arguments *args
**Question:** Create function that accepts any number of arguments and returns their sum.  
**Explanation:** Use *args to handle variable number of positional arguments.  
**Input:** Function call with 1, 2, 3, 4, 5  
**Output:** Sum of all arguments  
**Answer:** 15

```python
def factorial(*args):
    sum_var = sum(args)
    return sum_var

result = factorial(1, 2, 3, 4, 5)
print(result)
```

## 109. Keyword Arguments **kwargs
**Question:** Create function that accepts keyword arguments and returns them as dictionary.  
**Explanation:** Use **kwargs to capture arbitrary keyword arguments.  
**Input:** Function call with name="Alice", age=30  
**Output:** Dictionary of kwargs  
**Answer:** {'name': 'Alice', 'age': 30}

```python
name = input("Enter your Name:")
age = int(input("Enter your Age:"))

def kewargs_func(**kwargs):
    return kwargs
func= kewargs_func(name=name, age=age)
print(func)
```

## 110. Global vs Local Variables
**Question:** Create a global variable x=10, modify it inside a function.  
**Explanation:** Demonstrate global keyword usage for modifying global variables.  
**Input:** Global x=10, modify to 20 in function  
**Output:** Global variable value after function call  
**Answer:** 20

```python
x=10
def global_local(*args):
    global x
    x=20
    return x
print(global_local())
print(x)
```

## 111. List of Lists Flattening
**Question:** Flatten [[1, 2], [3, 4], [5, 6]] into single list.  
**Explanation:** Convert nested list structure into flat list.  
**Input:** [[1, 2], [3, 4], [5, 6]]  
**Output:** Flattened list  
**Answer:** [1, 2, 3, 4, 5, 6]

```python
faltten_list = [[1, 2], [3, 4], [5, 6]]
new_list = []
for i in faltten_list:
    if not isinstance(i, list):
        new_list.append(i)
    for j in i:
        if not isinstance(j, list):
            new_list.append(j)
print(new_list)

faltten_list = [10,11,12,13,[1, 2], [3, 4], [5, 6]]
new_list = []
for i in faltten_list:
    if isinstance(i, list):
        new_list.extend(i)
    else:
        new_list.append(i)

n = len(new_list)
print(new_list)

for i in range(n):
    for j in range(0, n-i-1):
        if new_list[j]>new_list[j+1]:
            temp = new_list[j]
            new_list[j] =new_list[j+1]
            new_list[j+1] = temp
print(new_list)
```

## 112. String Palindrome Check
**Question:** Check if "racecar" is a palindrome.  
**Explanation:** Compare string with its reverse to test palindrome property.  
**Input:** "racecar"  
**Output:** Boolean result  
**Answer:** True

```python
var_str = "racecar"
reverse_str = var_str[::-1]
print(reverse_str)

var_str = "racecar"
len_str = len(var_str)

def reverse_string(s):
    if s =="" or len_str==1:
        return s

    return reverse_string(s[1:])+s[0]

print(reverse_string(var_str))
```

## 113. Factorial Calculation
**Question:** Calculate factorial of 5.  
**Explanation:** Compute the product of all positive integers from 1 to n.  
**Input:** 5  
**Output:** Factorial value  
**Answer:** 120

```python
def factorial_calculate(n):
    result = 1
    for i in range(1, n+1):
        result *=i
    return result
variables = factorial_calculate(5)
print(variables)

def factorial_calculate(n):
    if n==0 or n==1:
        return 1
    return n* factorial_calculate(n-1)
variables = factorial_calculate(5)
print(variables)
```

## 114. Fibonacci Sequence
**Question:** Generate first 10 numbers in Fibonacci sequence.  
**Explanation:** Create sequence where each number is sum of previous two.  
**Input:** Count of 10  
**Output:** Fibonacci numbers  
**Answer:** [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]

```python
def fibonacci_sequence(n):
    fib = [0,1]
    for i in range(2,n):
        fib.append(fib[i-1] + fib[i-2])
    return fib[:n]

print(fibonacci_sequence(10))

def fibonacci_recursive(n):
    if n <= 1:
        return n
    return fibonacci_recursive(n-1) + fibonacci_recursive(n-2)
print([fibonacci_recursive(i) for i in range(10)])

def fibonacci_dp(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci_dp(n-1, memo) + fibonacci_dp(n-2, memo)
    return memo[n]

print([fibonacci_dp(i) for i in range(10)])

def fibonacci_sequence(n):
    fib = [0,1]
    for i in range(2,n):
        fib.append(fib[i-1] + fib[i-2])
    return fib[:n]
fibonacci= fibonacci_sequence(20)
print(fibonacci[10:20])

def fibonacci_range(start, end):
    fib = [0,1]
    for i in range(2, end+1):
        print(i, "list of i")
        print([i-1], "decrease 1")
        print([i-2], "decrease 2")
        print([i-1]+[i-2], "get values")
        print(fib)
        fib.append(fib[i-1] + fib[i-2])
    return fib[start:end+1]
fibonacci = fibonacci_range(10,20)
print(fibonacci)

def fibonacci_up_to(n):
    fib =[0,1]
    for i in range(2, n+1):
        fib.append(fib[i-1]+fib[i-2])
    return fib

def fibonacci_custom(indics):
    print(indics)
    max_index = max(indics)
    print(max_index)
    fib =fibonacci_up_to(max_index)
    return [fib[i] for i in indics]

custom_indices = [2, 4, 6, 7, 8, 9, 10, 11, 29, 4]
print(fibonacci_custom(custom_indices))
```

## 115. Prime Number Check
**Question:** Check if 17 is a prime number.  
**Explanation:** Test if number has no divisors other than 1 and itself.  
**Input:** 17  
**Output:** Boolean result  
**Answer:** True

```python
def is_prime(n):
    if n<2:
        return False
    for i in range(2, int(n**0.5) +1):
        print(i)
        if n%i==0:
            return False
    return True
print(is_prime(18))
```

## 116. String Anagram Check
**Question:** Check if "listen" and "silent" are anagrams.  
**Explanation:** Compare sorted characters of both strings.  
**Input:** "listen", "silent"  
**Output:** Boolean result  
**Answer:** True

```python
def are_anagrams(str1, str2):
    # Step 1: Remove spaces & convert to lowercase (optional)
    str1 = str1.replace(" ", "").lower()
    str2 = str2.replace(" ", "").lower()

    # Step 2: Compare sorted characters
    return sorted(str1) == sorted(str2)

# Example
print(are_anagrams("listen", "silent"))  # Output: True
```

## 117. List Rotation
**Question:** Rotate [1, 2, 3, 4, 5] to the right by 2 positions.  
**Explanation:** Move elements circularly to the right by specified positions.  
**Input:** [1, 2, 3, 4, 5], rotate by 2  
**Output:** Rotated list  
**Answer:** [4, 5, 1, 2, 3]

```python
def list_roatation(list_var, k):
    n = len(list_var)
    k = k%n
    return list_var[-k:] + list_var[:-k]
list_var = [1,2,3,4,5]
variables = list_roatation(list_var, 2)
print(variables)
```

## 119. Remove Duplicates
**Question:** Remove duplicates from [1, 2, 2, 3, 3, 4] preserving order.  
**Explanation:** Create new list with unique elements in original order.  
**Input:** [1, 2, 2, 3, 3, 4]  
**Output:** List without duplicates  
**Answer:** [1, 2, 3, 4]

```python
lst = [1, 2, 2, 3, 3, 4]

new_list = []

for i in lst:
    is_duplicate = False
    for u in new_list:
        if i == u:
            is_duplicate=True
            break
    if not is_duplicate:
        new_list.append(i)
print(new_list)
```

## 120. Dictionary Merge
**Question:** Merge {'a': 1, 'b': 2} and {'c': 3, 'b': 4}.  
**Explanation:** Combine dictionaries with second dict values taking precedence.  
**Input:** {'a': 1, 'b': 2} and {'c': 3, 'b': 4}  
**Output:** Merged dictionary  
**Answer:** {'a': 1, 'b': 4, 'c': 3}

```python
dict1 = {'a': 1, 'b': 2}
dict2 = {'c': 3, 'b': 4}
merge_dict = {}

for key in dict1:
    merge_dict[key] = dict1[key]

for key in dict2:
    merge_dict[key] = dict2[key]

print(merge_dict)
```

---

## Summary

This README contains 120 Python programming exercises covering fundamental concepts including:

- Basic operations and data types
- String manipulation
- List and tuple operations
- Dictionary and set operations
- Control flow (if-else, loops)
- Functions and lambda expressions
- Exception handling
- List/dictionary comprehensions
- Built-in functions
- Advanced topics like recursion and algorithms

Each exercise includes the question, explanation, expected input/output, and complete code solution. These exercises provide a comprehensive foundation for learning Python programming concepts from basic to intermediate level.
