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

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/RazvanBengaGemini/Swift-Style-Guide/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
