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

Use one or two uppercase letters such as T, U, or VM.

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
