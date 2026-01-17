# Sorting Visualizer

An interactive, educational sorting algorithm visualizer built with HTML, CSS, and JavaScript. Watch how different sorting algorithms work step by step, control the speed, and compare their time and space complexities in real time. This project supports six popular sorting algorithms with customizable array sizes, speed controls, and real-time complexity display.

## 🚀 Live Demo
Check it out here:  
[https://subhamdagar73.github.io/sorting_visualizer/](https://sorting-visualizer-lac-delta.vercel.app/)

## 🎯 Features
- **Interactive Animations** - Visualize each comparison and swap as the algorithm progresses with color-coded operations
- **Speed Controls** - Adjust animation speed on the fly (5 different speed levels)
- **Array Size Customization** - Adjust array size between 20-150 elements
- **Complexity Display** - Real-time display of best, average, and worst-case time & space complexities
- **Multiple Algorithms** - Bubble Sort, Selection Sort, Insertion Sort, Merge Sort, Quick Sort, and Heap Sort
- **Responsive Design** - Works seamlessly on desktop and tablet viewports
- **Visual Feedback** - Color-coded visualization:
  - **Yellow** - Current element being compared
  - **Red** - Elements being swapped
  - **Green** - Sorted elements
  - **Blue** - Unsorted elements

## 📁 Folder Structure
```
sorting_visualizer/
├── index.html              # Main HTML file
├── style.scss              # SCSS stylesheet source
├── css/
│   └── style.css           # Compiled CSS stylesheet
├── scripts/
│   ├── main.js             # Main application logic
│   ├── visualizations.js   # Animation and visualization utilities
│   ├── bubble_sort.js      # Bubble sort implementation
│   ├── selection_sort.js   # Selection sort implementation
│   ├── insertion_sort.js   # Insertion sort implementation
│   ├── merge_sort.js       # Merge sort implementation
│   ├── quick_sort.js       # Quick sort implementation
│   └── heap_sort.js        # Heap sort implementation
└── README.md               # This file
```

## 🚀 Getting Started

### Prerequisites
- A modern web browser (Chrome, Firefox, Safari, Edge)
- No additional dependencies or installations required

### Installation
1. Clone the repository:
```bash
git clone https://github.com/subhamdagar73/sorting_visualizer.git
cd sorting_visualizer
```

2. Open the application:
- Simply open `index.html` in your web browser, or
- Use a local server (recommended):
```bash
# Using Python 3
python -m http.server 8000

# Using Python 2
python -m SimpleHTTPServer 8000

# Using Node.js (with http-server package)
npx http-server
```

3. Navigate to `http://localhost:8000` in your browser

## 📖 How to Use

1. **Select Array Size** - Use the size slider (20-150) to adjust the number of elements
2. **Adjust Speed** - Use the speed slider (1-5) to control animation speed
3. **Generate New Array** - Click "Generate New Array!" button to create a random array
4. **Choose Algorithm** - Click on any sorting algorithm button to visualize it:
   - Bubble
   - Selection
   - Insertion
   - Merge
   - Quick
   - Heap
5. **Watch the Visualization** - The algorithm will automatically animate with color-coded operations
6. **View Complexities** - Check the left and right panels for time and space complexity information

## 🔍 Sorting Algorithms Overview

### Bubble Sort
- **Time Complexity**: O(N²) worst/average, O(N) best
- **Space Complexity**: O(1)
- **Description**: Repeatedly steps through the list, compares adjacent elements, and swaps them if in wrong order

### Selection Sort
- **Time Complexity**: O(N²) for all cases
- **Space Complexity**: O(1)
- **Description**: Selects the minimum element from unsorted portion and places it at the beginning

### Insertion Sort
- **Time Complexity**: O(N²) worst/average, O(N) best
- **Space Complexity**: O(1)
- **Description**: Builds sorted array by inserting elements one at a time into their correct position

### Merge Sort
- **Time Complexity**: O(N log N) for all cases
- **Space Complexity**: O(N)
- **Description**: Divide-and-conquer algorithm that divides array into halves, sorts them, and merges

### Quick Sort
- **Time Complexity**: O(N²) worst, O(N log N) average, O(N log N) best
- **Space Complexity**: O(log N)
- **Description**: Divide-and-conquer algorithm using pivot partitioning

### Heap Sort
- **Time Complexity**: O(N log N) for all cases
- **Space Complexity**: O(1)
- **Description**: Uses max heap to sort elements by repeatedly extracting maximum and placing at end

## 🛠️ Technologies Used
- **HTML5** - Structure and markup
- **CSS3** - Styling and responsive design
- **SCSS** - CSS preprocessor for style.scss
- **JavaScript (Vanilla)** - Algorithm implementations and animations
- **DOM API** - For dynamic element manipulation and styling

## 🐛 Known Issues & Limitations
- Quick sort may not perform optimally with certain pivot selection strategies on nearly sorted arrays
- Animations on very large arrays (150+ elements) may slow down depending on browser performance
- Mobile responsiveness could be improved for smaller screens

## 💡 How It Works
1. The application generates a random array and displays it as bars of varying heights
2. When an algorithm is selected, it performs sorting operations with animated visualization
3. Each comparison/swap is highlighted with colors and timed delays using `setTimeout()`
4. The `div_update()` function handles all visual updates with proper delay timing
5. Complexity information is displayed in real-time based on the selected algorithm





