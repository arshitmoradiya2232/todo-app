# Agent Instructions for Todo App

## Project Overview
A lightweight, single-file todo application built with vanilla HTML, CSS, and JavaScript. Features include:
- **Add/Delete/Complete todos** with optional due dates
- **Light/Dark theme** toggle with persistence
- **localStorage** for data persistence across sessions
- **Responsive design** with animations and smooth transitions

## Architecture

### Single File Structure
The entire app lives in `index.html` with three sections:
1. **HTML** (lines 358-382): Minimal DOM - header, input fields, todo list, empty message
2. **CSS** (lines 8-356): Embedded styles with CSS custom properties for theming
3. **JavaScript** (lines 383-580): All app logic

### Key Functions

**Data Management:**
- `loadTodos()` - Retrieve todos from localStorage (JSON parsed)
- `saveTodos(todos)` - Persist todos array to localStorage
- `renderTodos()` - Re-render entire todo list UI

**Todo Operations:**
- `addTodo()` - Create new todo, validate input, save and re-render
- `deleteTodo(index)` - Remove by index, save and re-render
- `toggleTodo(index)` - Toggle completed status, save and re-render

**Theme & Utilities:**
- `toggleTheme()` - Switch theme, update localStorage and icon
- `formatDate(dateString)` - Display "Today", "Tomorrow", or formatted date
- `escapeHtml(text)` - Prevent XSS by escaping HTML in todo text

## Development Patterns

### Storage
- Use `localStorage.getItem/setItem('todos')` for persistence
- Store todos as array of objects: `{text, dueDate, completed}`
- `dueDate` is optional (null if not set)

### DOM Updates
- Always call `renderTodos()` after any data change (add/delete/toggle)
- The function rebuilds the entire list - it's idempotent and safe
- Empty message visibility is managed in `renderTodos()`

### Events
- **Click events**: Add button, checkboxes, delete buttons, text to toggle
- **Keyboard**: Enter key on input to add todo
- **Theme**: Toggle button saves to localStorage immediately

### Theme System
- CSS custom properties (--variables) handle light/dark switching
- `data-theme` attribute on `<html>` (set to "light" or "dark")
- Save theme preference to localStorage for persistence

## Important Constraints

- **Single file**: Keep all CSS and JS embedded in index.html
- **No dependencies**: Pure vanilla JavaScript, no frameworks or libraries
- **XSS prevention**: Always use `escapeHtml()` or `.textContent` for user input (not `.innerHTML`)
- **localStorage only**: No backend, all data stored locally in browser

## Common Tasks

**Adding a feature**: Update HTML, add CSS variables for theming, implement function, add event listener

**Fixing bugs**: Check `renderTodos()` is called after data changes, verify localStorage read/write

**Styling**: Use CSS custom properties so light/dark themes are consistent. Test both themes.

**Testing**: Open in browser, test add/delete/toggle/theme toggle, check localStorage in DevTools
