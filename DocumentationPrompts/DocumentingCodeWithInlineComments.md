# Documenting Code with Inline Comments

## Prompt 1: Writing Effective Code Comments
```
Intent: To help developers write clear and helpful inline comments in their code.

Context: You are adding comments to a code file to improve its readability and maintainability. The code details are as follows:

Code_snippet: {code_snippet}
Programming_language: {programming_language}

Generate inline comments for the code, including:
- Function/method purpose comments.
- Complex logic explanations.
- Important variable descriptions.

Example:
Code_snippet:
```python
def process_data(raw_data):
    cleaned_data = []
    for item in raw_data:
        if item and not item.startswith('#'):
            parsed = item.strip().lower()
            if parsed not in cleaned_data:
                cleaned_data.append(parsed)
    return cleaned_data
```
Programming_language: "Python"

Commented Code:
```python
def process_data(raw_data):
    """
    Process and clean raw data by removing comments, whitespace, and duplicates.
    
    Args:
        raw_data: A list of string items to be processed
        
    Returns:
        A list of cleaned and unique data items
    """
    # Initialize empty list for storing cleaned data
    cleaned_data = []
    
    # Iterate through each item in the raw data
    for item in raw_data:
        # Skip empty items and comments (items starting with #)
        if item and not item.startswith('#'):
            # Clean the item by removing whitespace and converting to lowercase
            parsed = item.strip().lower()
            
            # Add the item to our result list if it's not already there
            if parsed not in cleaned_data:
                cleaned_data.append(parsed)
                
    return cleaned_data
```
```