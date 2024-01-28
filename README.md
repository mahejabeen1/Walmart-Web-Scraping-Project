# Walmart Web Scraping Project

## Purpose

This project aims to scrape the top 10 keywords from the titles of products on Walmart's website and visualize them using a WordCloud. The analysis provides insights into popular keywords found in product titles on Walmart.

## Steps to Run the Code

### 1. Setting Up the Environment

Make sure you have a Jupyter Notebook environment or Google Colab with the necessary libraries installed. If using Google Colab, create a new notebook and run the following commands in separate cells:

!pip install requests

!pip install beautifulsoup4

!pip install pandas

!pip install matplotlib

!pip install wordcloud

import requests

from bs4 import BeautifulSoup

import seaborn as sns

import pandas as pd

import matplotlib.pyplot as plt

### 2. Scraping Data
In a code cell, run the following code to scrape titles from Walmart's website:

url = "https://www.walmart.com"

response = requests.get(url)

soup = BeautifulSoup(response.text, 'html.parser')

data = {'Title': [soup.title.text]}

df = pd.DataFrame(data)

df['Title'] = df['Title'].astype(str)

# Split the strings, explode, and count the values

top_keywords = df['Title'].str.split().explode().value_counts().head(10)

print(top_keywords)

unique_words = df['Title'].str.split().explode().unique()

print(unique_words)

### 3. Data Analysis and Visualization
Continue with the following code to organize the data into a DataFrame:

sns.barplot(x=top_keywords.index, y=top_keywords.values)

plt.title('Top 10 Keywords in Titles')

plt.xlabel('Keywords')

plt.ylabel('Frequency')

plt.xticks(rotation=45, ha='right')

plt.show()

Here we scrape the visible text from Walmart's website using BeautifulSoap and Structure and organize the data in pandas-dataframe

# Extract the visible text
text = soup.get_text(separator=' ')

# Print the extracted text
print(text)

data = {'Title': [soup.get_text(separator=' ')]}

df = pd.DataFrame(data)

df['Title'] = df['Title'].astype(str)

top_keywords = df['Title'].str.split().explode().value_counts().head(10)
print(top_keywords)

# Print top 10 keywords in the visible text and their frequency in the visualization chart
sns.barplot(x=top_keywords.index, y=top_keywords.values)

plt.title('Top 10 Words in The Visible Text')

plt.xlabel('Keywords')

plt.ylabel('Frequency')

plt.xticks(rotation=45, ha='right')

plt.show()

