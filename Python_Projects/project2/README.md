This repository contains a Python script that generates and visualizes fuzzy membership functions for temperature categories. The fuzzy logic approach is used to represent different states of temperature (Cold, Warm, Hot) using triangular membership functions. The plot is saved as an image file.

Prerequisites
Before running the script, ensure you have the following Python libraries installed:

matplotlib (for plotting the graph)
numpy (for numerical computations)
scikit-fuzzy (for fuzzy logic operations)
You can install these dependencies using pip:

bash
Copy code
pip install matplotlib numpy scikit-fuzzy
Usage
Script Overview
The script defines a temperature range and creates fuzzy membership functions for three temperature categories:

Cold (temp_lo)
Warm (temp_md)
Hot (temp_hi)
These fuzzy sets are represented by triangular membership functions using the skfuzzy.trimf() function. The plot visualizes the temperature ranges and their membership values. The plot is then saved as an image (fuzzy_membership.png).

Step-by-Step Execution
Set Up Temperature Range: The temperature range (x_temp) is defined from 0 to 10, with steps of 1, representing the universe of discourse for temperature.

Generate Triangular Membership Functions: Three fuzzy sets are created using the fuzz.trimf() function:

Cold (temp_lo): A membership function with a peak at 0, and it decreases linearly to 0 at 5.
Warm (temp_md): A membership function with a peak at 5, and it decreases to 0 at 0 and 10.
Hot (temp_hi): A membership function with a peak at 10, and it decreases to 0 at 5.
Visualize the Membership Functions: The script uses matplotlib to plot the fuzzy membership functions:

The "Cold" membership function is plotted as a blue dashed line.
The "Warm" membership function is plotted as a green solid line.
The "Hot" membership function is plotted as a red dotted line.
The plot is labeled with a title ("Temperature") and includes a legend for each membership function.

Save the Plot: The plot is saved as a PNG image (fuzzy_membership.png) with a resolution of 100 DPI.

Output: The script will print messages to indicate when the plot is being saved and when the process is complete.

Running the Script
Save the script to a Python file, e.g., fuzzy_temperature.py.
Run the script from the command line:
bash
Copy code
python test_fuzzy.py
Output
The script will generate the following:

A plot showing the membership functions for Cold, Warm, and Hot temperature categories.
A PNG image file named fuzzy_membership.png saved in the current directory.
Example Output
The generated plot will display three triangular curves:

Cold (Blue dashed line): Membership function that peaks at 0.
Warm (Green solid line): Membership function that peaks at 5.
Hot (Red dotted line): Membership function that peaks at 10.