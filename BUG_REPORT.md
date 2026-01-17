# Bug Report - Sorting Visualizer

## Summary of Bugs Found

This document details bugs and issues discovered in the Sorting Visualizer application.

---

## 🔴 Critical Bugs

### 1. **Missing Variable Declaration in Selection Sort**
**File**: [scripts/selection_sort.js](scripts/selection_sort.js#L12)  
**Severity**: CRITICAL  
**Issue**: The variable `index_min` is used without being declared (no `var`, `let`, or `const`)

```javascript
index_min=i;  // Line 12 - Missing variable declaration
```

**Impact**: Creates a global variable, causing potential variable pollution and unexpected behavior in strict mode.

**Fix**: Add proper variable declaration:
```javascript
var index_min=i;
```

---

### 2. **Array Index Out of Bounds in Selection Sort**
**File**: [scripts/selection_sort.js](scripts/selection_sort.js#L45)  
**Severity**: CRITICAL  
**Issue**: After the loop completes, `i` equals `array_size-1`, but the code tries to access `divs[i]` and `div_sizes[i]` which is valid but should check bounds

The real issue is at line 45:
```javascript
div_update(divs[i],div_sizes[i],"green");//Color update
```

When the outer loop ends, `i = array_size - 1`, which is valid. However, the second update below it uses `i` which is now out of loop scope in a confusing way.

**Impact**: Minor - last element gets colored, but the code logic is unclear.

---

### 3. **Quick Sort - Incorrect Pivot Coloring**
**File**: [scripts/quick_sort.js](scripts/quick_sort.js#L48-L51)  
**Severity**: HIGH  
**Issue**: The loop that colors elements as sorted has an off-by-one error:

```javascript
for(var t=start;t<=i;t++)  // Line 48 - Colors from start to pivot position
{
    div_update(divs[t],div_sizes[t],"green");//Color update
}
```

The variable `i` is used but should be checking the pivot position more carefully. The loop marks elements as sorted even though they might not be in final sorted position.

**Impact**: Misleading visual representation during quicksort execution - elements are marked as sorted before they actually are in their final positions.

---

### 4. **Heap Sort - Missing Final Element Coloring**
**File**: [scripts/heap_sort.js](scripts/heap_sort.js#L88)  
**Severity**: MEDIUM  
**Issue**: In the final loop, the variable `i` goes out of scope after the loop:

```javascript
for(var i=array_size-1;i>0;i--)  // Line 71
{
    // ... operations ...
}
div_update(divs[i],div_sizes[i],"green");//Line 88 - i is -1 here!
```

After the loop completes, `i` equals `-1`, so `divs[-1]` and `div_sizes[-1]` are accessed, causing undefined behavior.

**Impact**: The first element (index 0) never gets marked as green (sorted), and the code attempts to access invalid array indices.

**Fix**: Should color `divs[0]` instead:
```javascript
div_update(divs[0],div_sizes[0],"green");//Color update
```

---

## 🟡 Moderate Bugs

### 5. **Missing Variable Declaration in Insertion Sort**
**File**: [scripts/insertion_sort.js](scripts/insertion_sort.js)  
**Severity**: MEDIUM  
**Issue**: Variables `key` and `i` are properly declared, but the overall structure could be clearer. However, there's a logic issue at the end:

```javascript
for(var t=0;t<j;t++)  // Lines 33-35 - Colors all elements up to j as green
```

This colors elements green multiple times (once per iteration), which is inefficient but not incorrect.

**Impact**: Performance impact due to redundant color updates; no functional bug.

---

## 🟡 Logic & Design Issues

### 6. **Global Variable Pollution**
**File**: [scripts/main.js](scripts/main.js)  
**Severity**: MEDIUM  
**Issue**: Multiple global variables are used across files:
- `c_delay`
- `div_sizes[]`
- `divs[]`
- `array_size`
- `margin_size`

Variables modified in one file affect others, making the code fragile and hard to maintain.

**Impact**: Difficult debugging, potential conflicts, poor code organization.

---

### 7. **No Reset of Variables Between Sorts**
**File**: [scripts/visualizations.js](scripts/visualizations.js#L21)  
**Severity**: MEDIUM  
**Issue**: The `c_delay` is reset to 0 at the start of each sorting function, but `delay_time` is calculated once. If you change the speed slider mid-sort, the timing may be inconsistent.

**Impact**: Unexpected animation timing if speed is adjusted during visualization.

---

### 8. **Race Condition in Button Enabling**
**File**: [scripts/visualizations.js](scripts/visualizations.js#L32-L40)  
**Severity**: MEDIUM  
**Issue**: The `enable_buttons()` function uses `setTimeout()` with the accumulated `c_delay`, but if multiple sorts are called quickly, timing could be off.

**Impact**: Buttons might be re-enabled before animation completes, allowing multiple simultaneous sorts.

---

## 🟢 Minor Issues

### 9. **Commented-Out Code**
**File**: [scripts/main.js](scripts/main.js#L8)  
**Severity**: LOW  
**Issue**: Unused commented line:
```javascript
//var array_speed=document.getElementById('a_speed').value;
```

**Fix**: Remove dead code or implement if needed.

---

### 10. **Inconsistent Comment Quality**
**File**: Multiple files  
**Severity**: LOW  
**Issue**: Comments have typos:
- [scripts/bubble_sort.js](scripts/bubble_sort.js#L29): "Color updat" (missing 'e')
- Inconsistent capitalization and formatting

**Fix**: Fix typos and standardize comment style.

---

### 11. **No Input Validation**
**Severity**: LOW  
**Issue**: No validation that array has elements before sorting:
```javascript
function Bubble() {
    // No check if array_size > 0 or divs.length > 0
}
```

**Impact**: Edge case handling missing for empty or single-element arrays.

---

## 🔧 Recommended Fixes Priority

| Priority | Bug | Fix Effort |
|----------|-----|-----------|
| 🔴 Critical | Missing `index_min` declaration | 5 min |
| 🔴 Critical | Heap sort final element bug | 5 min |
| 🟡 High | Quick sort sorting visualization | 10 min |
| 🟡 Medium | Global variable pollution | 30+ min (refactor) |
| 🟡 Medium | Race condition in button enabling | 15 min |
| 🟢 Low | Fix typos and comments | 5 min |
| 🟢 Low | Add input validation | 10 min |

---

## Testing Recommendations

1. Test each sorting algorithm with different array sizes (20, 50, 100, 150)
2. Change speed during visualization to test timing consistency
3. Verify all elements turn green when sort completes
4. Test in strict mode (`"use strict";`) to catch undeclared variables
5. Use browser developer tools console to check for any JavaScript errors

---

## Code Quality Improvements

1. **Use strict mode**: Add `"use strict";` at the top of files
2. **Refactor globals**: Use an object to namespace global variables
3. **Add error handling**: Check for edge cases and null values
4. **Improve maintainability**: Add more detailed comments and function documentation
5. **Modularize code**: Consider using modules or classes instead of global functions
