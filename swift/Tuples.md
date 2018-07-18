# What's a tuple?

A tuple is way of grouping multiple values into a single compound value. 

For example, say we wanted to represent an HTTP status code Interger, and it's description as a String. Instead of creating a Dictionary and storing those values in there, we can create a just-in-time data structure on the fly, or a tuple.

```swift
let http404Error = (404, "Not Found")
// http404Error is of type (Int, String), and equals (404, "Not Found")
```

The (404, "Not Found") tuple groups together an Int and a String to give the HTTP status code two separate values: a number and a human-readable description. It can be described as “a tuple of type (Int, String)”.

You can create tuples from any permutation of types, and they can contain as many different types as you like. There’s nothing stopping you from having a tuple of type (Int, Int, Int), or (String, Bool), or indeed any other permutation you require.

# How do they work?

You can decompose a tuple’s contents into separate constants or variables, which you then access as usual:

```swift
let (statusCode, statusMessage) = http404Error
print("The status code is \(statusCode)")
print("The status message is \(statusMessage)")
```

Alternatively, access the individual element values in a tuple using index numbers starting at zero:

```swift
print("The status code is \(http404Error.0)")
print("The status message is \(http404Error.1)")
```

You can name the individual elements in a tuple when the tuple is defined:

```swift
let http200Status = (statusCode: 200, description: "OK")
```

If you name the elements in a tuple, you can use the element names to access the values of those elements:

```swift
print("The status code is \(http200Status.statusCode)")
print("The status message is \(http200Status.description)")
```

Tuples are particularly useful as the return values of functions. A function that tries to retrieve a web page might return the (Int, String) tuple type to describe the success or failure of the page retrieval. By returning a tuple with two distinct values, each of a different type, the function provides more useful information about its outcome than if it could only return a single value of a single type. 

Here is an example of a method returning a tuple

```swift
func minMax(array: [Int]) -> (min: Int, max: Int) {
    var currentMin = array[0]
    var currentMax = array[0]
    for value in array[1..<array.count] {
        if value < currentMin {
            currentMin = value
        } else if value > currentMax {
            currentMax = value
        }
    }
    return (currentMin, currentMax)
}
```

## An example


```swift
func display(authError: Error?) {

        guard let code = AuthErrorCode(rawValue: (authError?._code)!) else {
            return
        }
        
        // tuple
        var error = (title: "", message: "")
        
        switch code {
            case .invalidEmail:
                print("Invalid email")
                error.title = "Invalid email"
                error.message = "Your email address was invalid"
            case .userNotFound:
                print("User not found")
                error.title = "User not found"
                error.message = "Your email address was entered was not found in the system"
            default:
                print("Internal error")
                error.title = "Internal error"
                error.message = "Something went wrong on our end"
        }
        
        let alert = UIAlertController(title: error.title, message: error.message, preferredStyle: .alert)
        
        let okAction = UIAlertAction(title: "OK", style: .default) { (action:UIAlertAction) in
            // nop
        }
        
        alert.addAction(okAction)
        
        present(alert, animated: true, completion: nil)
    }
```

### Links that help

* [Swift Lanaguage Guide - Basics](https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html)
