# Ex05 Image Carousel
## Date: 18-02-2026

## AIM
To create a Image Carousel using React 

## ALGORITHM
### STEP 1 Initial Setup:
Input: A list of images to display in the carousel.

Output: A component displaying the images with navigation controls (e.g., next/previous buttons).

### Step 2 State Management:
Use a state variable (currentIndex) to track the index of the current image displayed.

The carousel starts with the first image, so initialize currentIndex to 0.

### Step 3 Navigation Controls:
Next Image: When the "Next" button is clicked, increment currentIndex.

If currentIndex is at the end of the image list (last image), loop back to the first image using modulo:
currentIndex = (currentIndex + 1) % images.length;

Previous Image: When the "Previous" button is clicked, decrement currentIndex.

If currentIndex is at the beginning (first image), loop back to the last image:
currentIndex = (currentIndex - 1 + images.length) % images.length;

### Step 4 Displaying the Image:
The currentIndex determines which image is displayed.

Using the currentIndex, display the corresponding image from the images list.

### Step 5 Auto-Rotation:
Set an interval to automatically change the image after a set amount of time (e.g., 3 seconds).

Use setInterval to call the nextImage() function at regular intervals.

Clean up the interval when the component unmounts using clearInterval to prevent memory leaks.

## PROGRAM
### app.jsx
```
import React, { useState, useEffect } from "react";

function Carousel({ images }) {
  const [current, setCurrent] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setCurrent((prev) => (prev + 1) % images.length);
    }, 3000);

    return () => clearInterval(interval);
  }, [images.length]);

  return (
    <div className="carousel">

      {/* Main Image */}
      <div className="main-image">
        <img src={images[current]} alt="main" />
      </div>

      {/* Thumbnails */}
      <div className="thumbnails">
        {images.map((img, index) => (
          <img
            key={index}
            src={img}
            alt="thumb"
            className={current === index ? "active" : ""}
            onClick={() => setCurrent(index)}
          />
        ))}
      </div>

    </div>
  );
}

export default Carousel;
```
### image.jsx
```
import React, { useState, useEffect } from "react";

function Carousel({ images }) {
  const [current, setCurrent] = useState(0);

  // Auto slide
  useEffect(() => {
    const interval = setInterval(() => {
      setCurrent((prev) => (prev + 1) % images.length);
    }, 3000);

    return () => clearInterval(interval);
  }, [images.length]);

  return (
    <div className="carousel">

      {/* Main Image */}
      <div className="main-image">
        <img src={images[current]} alt="main" />
      </div>

      {/* Thumbnails */}
      <div className="thumbnails">
        {images.map((img, index) => (
          <img
            key={index}
            src={img}
            alt="thumb"
            className={current === index ? "active" : ""}
            onClick={() => setCurrent(index)}
          />
        ))}
      </div>

    </div>
  );
}

export default Carousel;
```
### index.css

```
body {
  margin: 0;
  font-family: Arial;
  background: #0f172a;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.carousel {
  width: 500px;
  text-align: center;
}

.main-image img {
  width: 100%;
  height: 300px;
  object-fit: cover;
  border-radius: 12px;
  box-shadow: 0 10px 25px rgba(0,0,0,0.5);
}

.thumbnails {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 15px;
}

.thumbnails img {
  width: 80px;
  height: 60px;
  object-fit: cover;
  border-radius: 6px;
  cursor: pointer;
  opacity: 0.6;
  transition: 0.3s;
}

.thumbnails img:hover {
  opacity: 1;
}

/* ACTIVE IMAGE */
.thumbnails img.active {
  border: 3px solid #38bdf8;
  opacity: 1;
}
```

## OUTPUT
<img width="1375" height="808" alt="image" src="https://github.com/user-attachments/assets/ba982aef-c672-44f9-b16e-18865fd54db9" />



## RESULT
The program for creating Image Carousel using React is executed successfully.
