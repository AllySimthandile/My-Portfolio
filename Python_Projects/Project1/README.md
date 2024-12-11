Description
The script generates random data for two predictor variables (X1 and X2) and simulates an outcome variable Y using a linear regression model:

 Y=α+β1.X1+β2.X2 +ϵ

Where:

α (alpha) is the intercept.
β1 and β2 are the coefficients of the predictor variables X1 and X2.
σ (sigma) is the standard deviation of the normally distributed noise, which is added to the outcome variable Y.
The code produces two scatter plots:

The first plot shows the relationship between X1 and Y.
The second plot shows the relationship between X2 and Y.
The generated plots are saved as a PNG file named predict.png.

Requirements
To run this script, you will need the following Python libraries:

numpy (for data generation and mathematical operations)
matplotlib (for plotting)
You can install the required libraries using pip:

bash
Copy code
pip install numpy matplotlib
Usage
Run the Python script:

bash
Copy code
python ch02_predict.py
The script will:

Generate random data for X1 and X2.
Simulate the outcome variable Y based on the specified linear regression model.
Create two scatter plots showing the relationship between X1/X2 and Y.
Save the figure as predict.png in the current working directory.
The script will print "finish" to the console once the process is complete.

Output
The script will generate a figure with two scatter plots and save it as predict.png in the working directory.
Example of Saved Plot:
X1 vs Y: Shows how X1 is related to the outcome variable Y.
X2 vs Y: Shows how X2 is related to the outcome variable Y.
Note:
The matplotlib.use('Agg') line ensures that the script can run without needing to display the plot on the screen (useful for running the script in headless environments).
Code Explanation
Data Generation:

X1 and X2 are generated using np.random.randn(), which creates standard normal random variables.
The outcome variable Y is simulated as a linear combination of X1, X2, and added noise (np.random.randn(size) * sigma).
Plotting:

The script creates two scatter plots using matplotlib.
The fig.subplots_adjust() method is used to adjust the layout to make the plots more readable.
The figure is saved to a PNG file using fig.savefig().