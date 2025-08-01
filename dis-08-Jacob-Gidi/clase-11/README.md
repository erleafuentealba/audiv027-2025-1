# clase-11

# Ejemplo 1

<!DOCTYPE html>
<html lang="en">
  <head>
    <script src="https://cdn.jsdelivr.net/npm/p5@1.11.7/lib/p5.js"></script>
    <script src="https://unpkg.com/ml5@1/dist/ml5.js"></script>
    <link rel="stylesheet" type="text/css" href="style.css">
    <meta charset="utf-8" />

  </head>
  <body>
    <main>
    </main>
    <script src="sketch.js"></script>
  </body>
</html>

# codigo 1
function setup() {
  createCanvas(640, 240);

  // Set the backend to 'webgl'
  ml5.setBackend("webgl");

  # codigo 2
  function setup() {
  ...
  classifier = ml5.neuralNetwork(options);

  // Add data to the neural network
  for (let i = 0; i < data.length; i++) {
    let item = data[i];

# Ejemplo 2

let classifier;

// Set the options for the neural network
let options = {
  task: "classification",
  debug: true,
};

let data = [
  { r: 255, g: 0, b: 0, color: "red-ish" },
  { r: 254, g: 0, b: 0, color: "red-ish" },
  { r: 253, g: 0, b: 0, color: "red-ish" },
  { r: 0, g: 255, b: 0, color: "green-ish" },
  { r: 0, g: 254, b: 0, color: "green-ish" },
  { r: 0, g: 253, b: 0, color: "green-ish" },
  { r: 0, g: 0, b: 255, color: "blue-ish" },
  { r: 0, g: 0, b: 254, color: "blue-ish" },
  { r: 0, g: 0, b: 253, color: "blue-ish" },
];

// Train the neural network
  const trainingOptions = {
    epochs: 32,
    batchSize: 12,
  };

function setup() {
  createCanvas(400, 400);
  // Set the backend to 'webgl'
  ml5.setBackend("webgl");

  classifier = ml5.neuralNetwork(options);

  // Add data to the neural network
  for (let i = 0; i < data.length; i++) {
    let item = data[i];
    
    let inputs = [item.r, item.g, item.b];
    
    let outputs = [item.color];
    
    classifier.addData(inputs, outputs);
    
    
    
  }
  
  classifier.normalizeData();
  
  classifier.train(trainingOptions, finishedTraining);
  
  
}

function draw() {
  background(220);
}

function finishedTraining() {
  classify();
}

function classify() {
  const input = [r, g, b];
  classifier.classify(input, handleResults);
}

# Ejemplo 3

let img;

// We will hold the totals for our color values here
let avgRed = 0;
let avgGreen = 0;
let avgBlue = 0;

// Load the image
function preload() {
  img = loadImage("mountain.jpg");
}

function setup() {
  createCanvas(400, 400);
  noStroke();

  // Resize the image to fit the canvas
  img.resize(width, height);

  // Load the pixels
  img.loadPixels();

  // Loop through the pixels X and Y
  for (let y = 0; y < img.height; y++) {
    for (let x = 0; x < img.width; x++) {

      // Calculate the pixel index
      const index = (y * img.width + x) * 4;

      // Sum the red, green, and blue values
      avgRed += img.pixels[index + 0];
      avgGreen += img.pixels[index + 1];
      avgBlue += img.pixels[index + 2];

    }
  }


  // We're finished working with pixels so update them
  img.updatePixels();

  // Get the total number of pixels
  // Divide by 4 because the total number of pixels = pixels * numColorChannels 
  const numPixels = img.pixels.length / 4;

  // divide the totals by the number of pixels to find the average.
  avgRed /= numPixels;
  avgGreen /= numPixels;
  avgBlue /= numPixels;
}

function draw() {

  // Draw the image as the background
  image(img, 0, 0);
  
  // Set the fill color to the average color of the pixels
  fill(avgRed, avgGreen, avgBlue);

  // Draw a square in the center of the screen
  rectMode(CENTER);
  rect(width / 2, height / 2, 100, 100);


}

# Ejemplo 4

let img;

// We will hold the totals for our color values here
let avgRed = 0;
let avgGreen = 0;
let avgBlue = 0;

// Load the image
function preload() {
  img = loadImage("flowers.jpg");
}

function setup() {
  createCanvas(400, 400);
  noStroke();

  // Resize the image to fit the canvas
  img.resize(width, height);

  // Load the pixels
  img.loadPixels();

  // Loop through the pixels X and Y
  for (let y = 0; y < img.height; y++) {
    for (let x = 0; x < img.width; x++) {

      // Calculate the pixel index
      const index = (y * img.width + x) * 4;

      // Sum the red, green, and blue values
      avgRed += img.pixels[index + 0];
      avgGreen += img.pixels[index + 1];
      avgBlue += img.pixels[index + 2];

    }
  }


  // We're finished working with pixels so update them
  img.updatePixels();

  // Get the total number of pixels
  // Divide by 4 because the total number of pixels = pixels * numColorChannels 
  const numPixels = img.pixels.length / 4;

  // divide the totals by the number of pixels to find the average.
  avgRed /= numPixels;
  avgGreen /= numPixels;
  avgBlue /= numPixels;
}

function draw() {

  // Draw the image as the background
  image(img, 0, 0);
  
  // Set the fill color to the average color of the pixels
  fill(avgRed, avgGreen, avgBlue);

  // Draw a square in the center of the screen
  rectMode(CENTER);
  rect(width / 2, height / 2, 100, 100);


}

# Ejemplo 5

/*
 * 👋 Hello! This is an ml5.js example made and shared with ❤️.
 * Learn more about the ml5.js project: https://ml5js.org/
 * ml5.js license and Code of Conduct: https://github.com/ml5js/ml5-next-gen/blob/main/LICENSE.md
 *
 * This example demonstrates training a color classifier through ml5.neuralNetwork.
 */

let img;

let avgRed = 0;
let avgGreen = 0;
let avgBlue = 0;

// Load the image
function preload() {
  img = loadImage("mountain.jpg");
}


// Step 1: load data or create some data
let data = [
  { r: 255, g: 0, b: 0, color: "red-ish" },
  { r: 254, g: 0, b: 0, color: "red-ish" },
  { r: 253, g: 0, b: 0, color: "red-ish" },
  { r: 0, g: 255, b: 0, color: "green-ish" },
  { r: 0, g: 254, b: 0, color: "green-ish" },
  { r: 0, g: 253, b: 0, color: "green-ish" },
  { r: 0, g: 0, b: 255, color: "blue-ish" },
  { r: 0, g: 0, b: 254, color: "blue-ish" },
  { r: 0, g: 0, b: 253, color: "blue-ish" },
];

let classifer;
let r = 255;
let g = 0;
let b = 0;
let label = "training";

function setup() {
  createCanvas(640, 240);
  
  
  

  // For this example to work across all browsers
  // "webgl" or "cpu" needs to be set as the backend
  ml5.setBackend("webgl");


  // Step 2: set your neural network options
  let options = {
    task: "classification",
    debug: true,
  };

  // Step 3: initialize your neural network
  classifier = ml5.neuralNetwork(options);

  // Step 4: add data to the neural network
  for (let i = 0; i < data.length; i++) {
    let item = data[i];
    let inputs = [item.r, item.g, item.b];
    let outputs = [item.color];
    classifier.addData(inputs, outputs);
  }

  // Step 5: normalize your data;
  classifier.normalizeData();

  // Step 6: train your neural network
  const trainingOptions = {
    epochs: 32,
    batchSize: 12,
  };
  classifier.train(trainingOptions, finishedTraining);
}
// Step 7: use the trained model
function finishedTraining() {
  classify();
}

// Step 8: make a classification
function classify() {
  const input = [avgRed, avgGreen, avgBlue];
  classifier.classify(input, handleResults);
  
  
  // Load the pixels
  img.loadPixels();

  // Loop through the pixels X and Y
  for (let y = 0; y < img.height; y++) {
    for (let x = 0; x < img.width; x++) {

      // Calculate the pixel index
      const index = (y * img.width + x) * 4;

      // Sum the red, green, and blue values
      avgRed += img.pixels[index + 0];
      avgGreen += img.pixels[index + 1];
      avgBlue += img.pixels[index + 2];

    }
  }


  // We're finished working with pixels so update them
  img.updatePixels();

  // Get the total number of pixels
  // Divide by 4 because the total number of pixels = pixels * numColorChannels 
  const numPixels = img.pixels.length / 4;

  // divide the totals by the number of pixels to find the average.
  avgRed /= numPixels;
  avgGreen /= numPixels;
  avgBlue /= numPixels;
  
  console.log(avgRed, avgGreen, avgBlue);

  
}

function draw() {
  
  background(avgRed, avgGreen, avgBlue);
  textAlign(CENTER, CENTER);
  textSize(64);
  text(label, width / 2, height / 2);
}

// Step 9: define a function to handle the results of your classification
function handleResults(results, error) {
  if (error) {
    // console.error(error);
    return;
  }
  label = results[0].label;
  classify();
}
