# Design Implementation Guidelines

## Prompt 1: Creating Component-Based UI Structure
```
Intent: To help developers implement UI designs using GitHub Copilot.

Context: You are implementing a UI design into code. The design details are as follows:

ui_framework: {ui_framework}
component_name: {component_name}
component_description: {component_description}

Generate component implementation code, including:
- Component structure
- Basic styling
- State management
- Event handlers

Example:
ui_framework: "React with CSS"
component_name: "SearchBar"
component_description: "A search input with a submit button, suggestions dropdown, and clear button"

Component Implementation:
```jsx
import React, { useState, useEffect } from 'react';
import './SearchBar.css';

const SearchBar = ({ onSearch, placeholder = "Search...", initialValue = "" }) => {
  const [search_term, setSearchTerm] = useState(initialValue);
  const [suggestions, setSuggestions] = useState([]);
  const [is_focused, setIsFocused] = useState(false);
  
  // Clear search input
  const handleClear = () => {
    setSearchTerm("");
    setSuggestions([]);
  };
  
  // Handle search submission
  const handleSubmit = (e) => {
    e.preventDefault();
    if (search_term.trim()) {
      onSearch(search_term);
      setIsFocused(false);
    }
  };
  
  // Handle input changes
  const handleChange = (e) => {
    const value = e.target.value;
    setSearchTerm(value);
    
    // Mock suggestion fetching - in a real app, this might be an API call
    if (value.length > 2) {
      const mock_suggestions = [
        `${value} example`,
        `${value} sample`,
        `${value} demo`
      ];
      setSuggestions(mock_suggestions);
    } else {
      setSuggestions([]);
    }
  };
  
  return (
    <div className="search-bar-container">
      <form onSubmit={handleSubmit} className="search-form">
        <div className="search-input-wrapper">
          <input
            type="text"
            value={search_term}
            onChange={handleChange}
            onFocus={() => setIsFocused(true)}
            placeholder={placeholder}
            className="search-input"
          />
          {search_term && (
            <button 
              type="button" 
              className="clear-button"
              onClick={handleClear}
            >
              ✕
            </button>
          )}
        </div>
        <button type="submit" className="search-button">
          Search
        </button>
      </form>
      
      {is_focused && suggestions.length > 0 && (
        <ul className="suggestions-list">
          {suggestions.map((suggestion, index) => (
            <li 
              key={index}
              onClick={() => {
                setSearchTerm(suggestion);
                onSearch(suggestion);
                setIsFocused(false);
              }}
              className="suggestion-item"
            >
              {suggestion}
            </li>
          ))}
        </ul>
      )}
    </div>
  );
};

export default SearchBar;
```

CSS Implementation:
```css
.search-bar-container {
  position: relative;
  width: 100%;
  max-width: 600px;
  margin: 0 auto;
}

.search-form {
  display: flex;
  align-items: center;
}

.search-input-wrapper {
  position: relative;
  flex: 1;
}

.search-input {
  width: 100%;
  padding: 10px 35px 10px 15px;
  border: 1px solid #ccc;
  border-radius: 4px 0 0 4px;
  font-size: 16px;
  outline: none;
}

.clear-button {
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  background: none;
  border: none;
  cursor: pointer;
  font-size: 14px;
  color: #888;
}

.search-button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 0 4px 4px 0;
  cursor: pointer;
  font-size: 16px;
}

.search-button:hover {
  background-color: #0056b3;
}

.suggestions-list {
  position: absolute;
  width: 100%;
  background: white;
  border: 1px solid #ddd;
  border-top: none;
  border-radius: 0 0 4px 4px;
  list-style-type: none;
  padding: 0;
  margin: 0;
  max-height: 200px;
  overflow-y: auto;
  z-index: 10;
}

.suggestion-item {
  padding: 10px 15px;
  cursor: pointer;
}

.suggestion-item:hover {
  background-color: #f5f5f5;
}
```

Key points to consider:
1. Focus on code structure and functionality rather than visual aspects
2. Use standard component patterns for the chosen framework
3. Include basic styling that can be easily customized
4. Implement common state management patterns
5. Use descriptive variable names with underscores for snake_case variables
```