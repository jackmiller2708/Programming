Refactoring is an important part of a developer’s day-to-day job. Ironically, OOP code is notoriously hard to refactor. Refactoring is supposed to make the code less complex, and more maintainable. On the contrary, refactored OOP code becomes significantly more complex — to make the code testable, we’d have to make use of dependency injection, and create an interface for the refactored class. Even then, refactoring OOP code is really hard without dedicated tools like Resharper.

In the simple example above, the line count has more than doubled just to extract a single method. Why does refactoring create even more complexity, when the code is being refactored in 
order to decrease complexity in the first place?

```Csharp
// before refactoring: 
public class CalculatorForm 
{ 
    private string aText, bText; 
    private bool IsValidInput(string text) => true; 
    
    private void btnAddClick(object sender, EventArgs e) 
    { 
        if(!IsValidInput(bText) || !IsValidInput(aText)) 
        { 
          return; 
        } 
    } 
} 
// after refactoring: 
public class CalculatorForm { 
    private string aText, bText; 
    private readonly IInputValidator _inputValidator; 
    
    public CalculatorForm(IInputValidator inputValidator) 
    { 
        _inputValidator = inputValidator; 
    } 
    
    private void btnAddClick(object sender, EventArgs e) 
    { 
        if(!_inputValidator.IsValidInput(bText) || !_inputValidator.IsValidInput(aText)) 
        { 
            return; 
        } 
    } 
} 

public interface IInputValidator 
{ 
    bool IsValidInput(string text); 
} 

public class InputValidator : IInputValidator 
{ 
    public bool IsValidInput(string text) => true; 
} 

public class InputValidatorFactory { 
    public IInputValidator CreateInputValidator() => new InputValidator(); 
}
```

Contrast this to a similar refactor of non-OOP code in JavaScript:

```JS
// before refactoring: 
// calculator.js: 
const isValidInput = text => true; 
const btnAddClick = (aText, bText) => { 
    if (!isValidInput(aText) || !isValidInput(bText)) { 
        return; 
    } 
} 

// after refactoring: 
// inputValidator.js: 
export const isValidInput = text => true; 

// calculator.js: 
import { isValidInput } from './inputValidator'; 

const btnAddClick = (aText, bText, _isValidInput = isValidInput) => { 
    if (!_isValidInput(aText) || !_isValidInput(bText)) { 
        return; 
    } 
}
```

The code has literally stayed the same — we simply moved the `isValidInput` function to a different file and added a single line to import that function. We’ve also added `_isValidInput` to the function signature for the sake of testability.

This is a simple example, but in practice the complexity grows exponentially as the codebase gets bigger.

And that’s not all. Refactoring OOP code is _extremely risky_. Complex dependency graphs and state scattered all over OOP codebase, make it impossible for the human brain to consider all of the potential issues.