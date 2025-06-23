# Ternary-plot-visualization
This project visualizes the specialization of research funders across three scientific domains using a ternary plot. It provides an intuitive, graphical way to understand funders’ focus areas in terms of:
Physiology Studies; Clinical Studies; Risk Factors & Diagnosis Techniques.
The plot divides the ternary space into six meaningful regions labeled A–F, each representing different combinations of specialization. The project is implemented in Python using Plotly for interactive plotting and Pandas for data manipulation.

To visualize the specialization of research funders in a ternary coordinate system, we first transform their RSI (Research Specialization Index) values into a form suitable for ternary plotting. This process ensures that each data point lies inside the triangle, meaning the values must be non-negative and sum to 1.

Here’s how this transformation is done:

Step 1: Offset Negative RSI Values
RSI values can be negative, but ternary plots require all inputs to be positive. To fix this, we calculate the minimum RSI value across all three fields (Physiology, Clinical Studies, Risk & Diagnosis Techniques), and shift all values by adding a small offset:

offset = abs(min(RSI values)) + 0.0001
df["RSI_x"] += offset  # for each dimension x

This ensures all values are positive without distorting their relative differences.

Step 2: Ternary Normalization (Convert to Proportions)
Next, for each funder, we calculate the sum of their three adjusted RSI values and divide each value by that sum:
df_sum = RSI_Physiology + RSI_CS + RSI_RD
df["RSI_Physiology"] /= df_sum
df["RSI_CS"] /= df_sum
df["RSI_RD"] /= df_sum
After this step, each funder’s specialization is represented as a proportion of total focus, satisfying the ternary plot condition:
RSI_Physiology + RSI_CS + RSI_RD = 1
This allows each funder to be plotted as a single point within the triangle, reflecting their relative emphasis on each research domain.
