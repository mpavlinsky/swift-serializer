# Swift Serializer
Apple Swift Strong Type Object Serialization to JSON

# Usage

```swift
import XCTest

class Person:Serializable {
    var Name : String
    var Surname : String
    var Animals : Array<Animal>
    
    init(Name:String, Surname:String) {
        self.Name = Name
        self.Surname = Surname
        self.Animals = Array<Animal>()
    }
}

class Animal:Serializable {
    var Nickname : String
    var Kind : String
    var Trick : String?

    init(Nickname : String, Kind : String, Trick : String?) {
        self.Nickname = Nickname
        self.Kind = Kind
        self.Trick = Trick
    }
}

class SerializationTests: XCTestCase {
    func test_serialization_works() {
        var john = Person(Name: "John", Surname: "Doe")
        
        john.Animals.append(Animal(Nickname: "Fluffy", Kind: "Dog", Trick: "Rollover"))
        john.Animals.append(Animal(Nickname: "Purry", Kind: "Cat", Trick: nil))
        
        println(john.toJson()) //will give binary data to include in HTTP Body
        println(john.toJsonString()) //will give the exact string in JSON
        
        var expected = "{\"Surname\":\"Doe\",\"Name\":\"John\",\"Animals\":[{\"Trick\":\"Rollover\",\"Kind\":\"Dog\",\"Nickname\":\"Fluffy\"},{\"Kind\":\"Cat\",\"Nickname\":\"Purry\"}]}";
        
        XCTAssertEqual(john.toJsonString(), expected,"")
    }
}
```

# Contributing
We will accept all valid Pull Requests, Feature Requests and any other Issues made on this project. Any questions just ask.
