Here is your Data Contract for the Digital Grade Checker in markdown format:

---

# Data Contract: Digital Grade Checker v1.0

## 1. Introduction

This document defines the data structure for a "Grade Check Result."  
Both the frontend visualizer (Path A) and backend engine (Path B) must strictly adhere to this contract.  
It enables decoupled development with a shared, stable interface.

---

## 2. Grade Check Result Object

This is the standard output produced by the core calculation logic.

**Example Object:**

```json
{
  "bucket_position": {
    "x": 65,
    "y": 15
  },
  "target_depth_at_x": 12.5,
  "vertical_delta": -2.5,
  "status": "too_deep"
}
```

---

## 3. Field Definitions

- **bucket_position (Object):** The input position analyzed.
  - **x (Number):** Horizontal position.
  - **y (Number):** Vertical position (depth).
- **target_depth_at_x (Number):** Calculated target depth at the bucket's x position.
- **vertical_delta (Number):** Vertical difference between bucket depth and target depth.  
  Negative value = bucket is below target (too deep).
- **status (String):** Final status of the bucket's position.  
  Allowed values:
  - `"on_grade"`
  - `"too_high"`
  - `"too_deep"`

---

## 4. Mock Data for Development

### Target Grade Plan

Use this data to represent the digital construction plan:

- From x=0 to x=50: flat at y=10
- From x=50 to x=100: slopes down from y=10 to y=20

```js
const targetGrade = [
  { x: 0, y: 10 },
  { x: 50, y: 10 },
  { x: 100, y: 20 }
];
```

---

### Self-Validating Test Cases

Use these for testing logic and visualization.  
"on_grade" status assumes a tolerance of +/- 0.25 units.

#### Test Case 1: "Too High"

- **Input:** `{ "position": { "x": 25, "y": 8 } }`
- **Reasoning:** At x=25, target depth is 10. Bucket at 8 is 2 units above target.
- **Expected status:** `"too_high"`

#### Test Case 2: "On Grade"

- **Input:** `{ "position": { "x": 75, "y": 15.1 } }`
- **Reasoning:** At x=75 (halfway on slope), target depth is 15. Bucket at 15.1 is within tolerance.
- **Expected status:** `"on_grade"`

#### Test Case 3: "Too Deep"

- **Input:** `{ "position": { "x": 90, "y": 20 } }`
- **Reasoning:** At x=90 (80% on slope), target depth is 18. Bucket at 20 is 2 units below target.
- **Expected status:** `"too_deep"`

---

**All prototypes must strictly follow this contract for compatibility and rapid feedback.**
