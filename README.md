# Project-12---Web-Scraping-With-Beautiful-Soup
import codecademylib3_seaborn
from bs4 import BeautifulSoup
import requests
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
#1
#2
webpage = requests.get("https://content.codecademy.com/courses/beautifulsoup/cacao/index.html")
#3
soup = BeautifulSoup(webpage.content, "html.parser")
#4
print(soup)
#5
ratings_tags = soup.find_all(attrs={"class": "Rating"})
#6
ratings = []
#7
for text in ratings_tags[1:]:
    ratings.append(float(text.get_text()))
#8
plt.hist(ratings)
plt.show()
#9
company_names_tags = soup.find_all(attrs={"class": "Company"})
#10
company = []
#11
for name in company_names_tags[1:]:
    company.append(name.get_text())
#12
df = pd.DataFrame.from_dict({"Company": company, "Rating": ratings})
#13
average_group_rating = df.groupby("Company").Rating.mean()
