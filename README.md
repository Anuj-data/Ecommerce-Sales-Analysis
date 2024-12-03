# **📊 Ecommerce Sales Analysis**  
**🔍 Analyzing Sales and Profit for Strategic Insights**  

---

## **📖 Introduction**  
This project focuses on analyzing ecommerce sales and profit data to derive actionable insights. Using Python, key trends, patterns, and relationships were identified, enabling businesses to enhance decision-making and strategic planning.

---

## **❓ Questions Answered**  
1. 📅 **Monthly Sales Analysis:** Which month had the highest and lowest sales?  
2. 📦 **Sales by Category:** Which product category had the highest and lowest sales?  
3. 🔎 **Sales by Sub-Category:** Performance analysis at the sub-category level.  
4. 📈 **Monthly Profit Trends:** Which month had the highest profit?  
5. 💰 **Profit by Category and Sub-Category:** Identifying profitable categories and sub-categories.  
6. 👥 **Sales and Profit by Customer Segment:** Understanding segment-level performance.  
7. 🧮 **Sales-to-Profit Ratio:** Measuring profitability efficiency.  

---

## **🛠️ Tools and Libraries Used**  
- **Python Libraries:**  
  - `pandas` for data manipulation.  
  - `plotly.express` and `plotly.graph_objects` for interactive visualizations.  
- **Dataset:** *Sample - Superstore.csv*, loaded and analyzed with `pandas`.  
- **Key Features:**  
  - Conversion of date columns to `datetime`.  
  - Additional columns created for better temporal analysis (e.g., `Order month`, `Order year`).  

---

## **❓ Questions Answered with Code**  

### **📅 1. Monthly Sales Analysis**  
**Which month had the highest and lowest sales?**  
```python
import pandas as pd 
import plotly.express as px
import plotly.graph_objects as go
import plotly.io as pio  
import plotly.colors as colors

# Set the default template
pio.templates.default = 'plotly_white'

# Load the dataset
data = pd.read_csv('Sample - Superstore.csv', encoding='latin-1')

# Analysis
sales_by_month = data.groupby('Order month')['Sales'].sum().reset_index()
fig = px.line(sales_by_month,
              x='Order month',
              y='Sales',
              title='Monthly sales analysis')
fig.show()
```
### **📦 2. Sales by Category**  
**Which product category had the highest and lowest sales?**  
```python
sales_by_category = data.groupby('Category')['Sales'].sum().reset_index()
fig = px.pie(
    sales_by_category,
    values='Sales',
    names='Category',
    hole=0.5,
    color_discrete_sequence=px.colors.qualitative.Pastel1
)

fig.update_traces(textposition='inside', textinfo='percent+label')
fig.update_layout(title_text='Sales analysis by category', title_font=dict(size=24))
fig.show()
```
### **🔎 3. Sales by Sub-Category**  
**Performance analysis at the sub-category level.**  
```python
sales_by_Subcategory = data.groupby('Sub-Category')['Sales'].sum().reset_index()
fig = px.bar(sales_by_Subcategory, x='Sub-Category', y='Sales', title='Sales analysis by sub category')
fig.show()
```
### **📈 4. Monthly Profit Trends**  
**Which month had the highest profit?**  
```python
profit_by_month = data.groupby('Order month')['Profit'].sum().reset_index()
fig = px.bar(profit_by_month, x='Order month', y='Profit', title='Analysis profit by month')
fig.show()
```
### **💰 5. Profit by Category and Sub-Category**  
**Identifying profitable categories and sub-categories.**  
```python
# By Category
profit_by_category = data.groupby('Category')['Profit'].sum().reset_index()
fig = px.pie(
    profit_by_category,
    values='Profit',
    names='Category',
    hole=0.5,
    color_discrete_sequence=px.colors.qualitative.Pastel1
)

fig.update_traces(textposition='inside', textinfo='percent+label')
fig.update_layout(title_text='Profit analysis by category', title_font=dict(size=24))
fig.show()

# By Sub-Category
profit_by_Subcategory = data.groupby('Sub-Category')['Profit'].sum().reset_index()
fig = px.bar(profit_by_Subcategory, x='Sub-Category', y='Profit', title='Profit analysis by Sub-Category')
fig.show()
```
### **👥 6. Sales and Profit by Customer Segment**  
**Understanding segment-level performance.**  
```python
sales_profit_by_segment = data.groupby('Segment').agg({'Sales': 'sum', 'Profit': 'sum'}).reset_index()
color_palette = colors.qualitative.Pastel

fig = go.Figure()

fig.add_trace(go.Bar(
    x=sales_profit_by_segment['Segment'],
    y=sales_profit_by_segment['Sales'],
    name='Sales',
    marker_color=color_palette[0]
))

fig.add_trace(go.Bar(
    x=sales_profit_by_segment['Segment'],
    y=sales_profit_by_segment['Profit'],
    name='Profit',
    marker_color=color_palette[1]
))

fig.update_layout(
    title='Sales and Profit Analysis by Customer Segment',
    xaxis_title='Customer Segment',
    yaxis_title='Amount',
    barmode='group'
)
fig.show()
```
### **🧮 7. Sales-to-Profit Ratio**  
**Measuring profitability efficiency.**  
```python
sales_profit_by_segment = data.groupby('Segment').agg({'Sales': 'sum', 'Profit': 'sum'}).reset_index()
sales_profit_by_segment['Sales_to_profit_ratio'] = sales_profit_by_segment['Sales'] / sales_profit_by_segment['Profit']
print(sales_profit_by_segment[['Segment', 'Sales_to_profit_ratio']])
```
### **🔑 Key Insights**  
**Monthly Trends:**  
- Highest sales occurred in November; lowest in February.  
- Monthly profits peaked in December.  

**Category and Sub-Category Analysis:**  
- Technology led in both sales and profit, while Office Supplies followed.  
- Sub-categories like "Tables" had negative profit, highlighting areas for cost optimization.  

**Segment Analysis:**  
- The Consumer segment showed the highest sales and profit.  

**Profitability:**  
- Sales-to-Profit ratio revealed efficient and inefficient segments.  

---

### **📊 Visualizations**  
- Line chart: Monthly sales trends.  
- Pie charts: Sales and profit by category.  
- Bar charts: Sub-category performance, monthly profits, and segment analysis.  

---

### **📝 Conclusion**  
This project demonstrates the power of Python for data analysis and visualization, enabling businesses to uncover insights and make data-driven decisions. Each question was systematically addressed, showcasing proficiency in Python and storytelling through data.
