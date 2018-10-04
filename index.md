## WHP Swift style guide

This style guide is based on the [raywenderlich.com Swift Style Guide](https://github.com/raywenderlich/swift-style-guide) and is meant to help us maintain consistency across projects and also provide a guideline for code review. We've also added SwiftLint as a static code ananlys tool but we should fallback to this style guide for cases that are not covered by SwiftLint. This is a work in progress so please feel free to contribute.

### Use Type Inferred Context

Use compiler inferred context to write shorter, clear code.

**Preferred:**
```
let selector = #selector(viewDidLoad)
view.backgroundColor = .red
let toView = context.view(forKey: .to)
let view = UIView(frame: .zero)
```

**Not Preferred:**
```
let selector = #selector(ViewController.viewDidLoad)
view.backgroundColor = UIColor.red
let toView = context.view(forKey: UITransitionContextViewKey.to)
let view = UIView(frame: CGRect.zero)
```

### Generic type paramateres and associated types

Use one or max two uppercase letters such as T, U, or VM.

**Preferred:**
```
struct Stack<V> { ... }
associatedType VM
```

**Not Preferred:**
```
struct Stack<View> { ... }
associatedType ViewModel
```

### Use of Self

For conciseness, avoid using self since Swift does not require it to access an object's properties or invoke its methods.

Use self only when required by the compiler (in @escaping closures, or in initializers to disambiguate properties from arguments). In other words, if it compiles without self then omit it.

### Closure Expressions

Use trailing closure syntax only if there's a single closure expression parameter at the end of the argument list. Give the closure parameters descriptive names.

**Preferred:**
```
UIView.animate(withDuration: 1.0) {
   self.myView.alpha = 0
}

UIView.animate(withDuration: 1.0, animations: {
   self.myView.alpha = 0
}, completion: { finished in
   self.myView.removeFromSuperview()
})
```

**Not Preferred:**
```
UIView.animate(withDuration: 1.0, animations: {
   self.myView.alpha = 0
})

UIView.animate(withDuration: 1.0, animations: {
   self.myView.alpha = 0
}) { f in
   self.myView.removeFromSuperview()
}
```

### Type Annotation for Empty Arrays and Dictionaries

For empty arrays and dictionaries, use type annotation. (For an array or dictionary assigned to a large, multi-line literal, use type annotation.)

**Preferred:**
```
var names: [String] = []
var lookup: [String: Int] = [:]
```

**Not Preferred:**
```
var names = [String]()
var lookup = [String: Int]()
```

### Syntactic Sugar

Prefer the shortcut versions of type declarations over the full generics syntax.

**Preferred:**
```
var deviceModels: [String]
var employees: [Int: String]
var faxNumber: Int?
```

**Not Preferred:**
```
var deviceModels: Array<String>
var employees: Dictionary<Int, String>
var faxNumber: Optional<Int>
```

### Unused Code

Unused (dead) code, including Xcode template code and placeholder comments should be removed.

**Preferred:**
```
override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    return Database.contacts.count
}
```

**Not Preferred:**
```
override func didReceiveMemoryWarning() {
    super.didReceiveMemoryWarning()
    // Dispose of any resources that can be recreated.
}

override func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
    // #warning Incomplete implementation, return the number of rows
    return Database.contacts.count
}
```

## Code organization

Use extensions to organize your code into logical blocks of functionality. Each extension should be set off with a // MARK: - comment to keep things well-organized.

### Protocol Conformance

When conforming to a protocol please add a separate extension for the protocol methods. This keeps the related methods grouped together with the protocol and can simplify instructions to add a protocol to a class with its associated methods.

**Preferred:**
```
class MyViewController: UIViewController {
    // class stuff here
}

// MARK: - UITableViewDataSource
extension MyViewController: UITableViewDataSource {
    // table view data source methods
}

// MARK: - UIScrollViewDelegate
extension MyViewController: UIScrollViewDelegate {
    // scroll view delegate methods
}
```

**Not Preferred:**
```
class MyViewController: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
    // all methods
}
```

### Classes/Structs properties and methods organization

We should organize our classes/structs body in the following order:

1. **IBOutlets** (only in the case of ViewControllers)
2. **Public/Internal properties** (please use public only when neccessary otherwise use the internal - default access modifier)
3. **FilePrivate and Private properties**
4. **LifeCycle methods** (only in the case of ViewControllers)
5. **IBActions** (only in the case of ViewControllers)
6. **Public/Internal Functions** (please use public only when neccessary otherwise use the internal - default access modifier)
7. **Private Functions**

**Preferred:**
```
class MyViewController: UIViewController {

    @IBOutlet weak var title: UILabel!
    @IBOutlet weak var subtitle: UILabel!
    
    var property1: String?
    private let property2: String
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }
    
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
    }
    
    @IBAction func someAction(_ sender: Any) {
    }
    
    func someFunc() {
    }
    
    private somePrivateFunc() {
    }
    
}
```

**Not Preferred:**
```
class MyViewController: UIViewController {

    var property1: String?
    
    @IBOutlet weak var title: UILabel!
    @IBOutlet weak var subtitle: UILabel!
    
    private let property2: String
    
    func someFunc() {
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }
    
    @IBAction func someAction(_ sender: Any) {
    }
    
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
    }
    
    private somePrivateFunc() {
    }
    
}
```

## Spacing

- Indent using tabs rather than spaces.
- Method braces and other braces (if/else/switch/while etc.) always open on the same line as the statement but close on a new line.

**Preferred:**
```
if user.isHappy {
    // Do something
} else {
    // Do something else
}
```

**Not Preferred:**
```
if user.isHappy
{
  // Do something
}
else {
  // Do something else
}
```

- Classes, structs, enums should have a top and a bottom whitespace.

**Preferred:**
```
class SomeClass {
    
    var property: String?
    
    func someFunc() {
    }
    
}
```

**Not Preferred:**
```
class SomeClass {
    var property: String?
    
    func someFunc() {
    }
}
```

- There should be exactly one blank line between methods to aid in visual clarity and organization. Whitespace within methods should separate functionality, but having too many sections in a method often means you should refactor into several methods (No top/bottom whitespace needed).

- Colons always have no space on the left and one space on the right. Exceptions are the ternary operator ? :, empty dictionary [:] and #selector syntax for unnamed parameters (_:).

**Preferred:**
```
class TestDatabase: Database {
    var data: [String: CGFloat] = ["A": 1.2, "B": 3.2]
}
```

**Not Preferred:**
```
class TestDatabase : Database {
    var data :[String:CGFloat] = ["A" : 1.2, "B":3.2]
}
```
