# Web-Scrapping-using-BeautifulSoup

# Required packages 
import bs4
import requests
import time
import random as ran
import sys
import pandas as pd

#  top 1000 films released in year of 2018 at imdb.com and scrapping 
url = 'https://www.imdb.com/search/title?release_date=2018&sort=boxoffice_gross_us,desc&start=1'

source = requests.get(url).text
soup = bs4.BeautifulSoup(source,'html.parser') # this code finds 


# only finding movie information from above page
movie_blocks = soup.findAll('div',{'class':'lister-item-content'})

# only first movie
mname = movie_blocks[0].find('a').get_text() # Name of the movie

m_reyear = int(movie_blocks[0].find('span',{'class': 'lister-item-year'}).contents[0][1:-1]) # Release year

m_rating = float(movie_blocks[0].find('div',{'class':'inline-block ratings-imdb-rating'}).get('data-value')) #rating

m_mscore = float(movie_blocks[0].find('span',{'class':'metascore favorable'}).contents[0].strip()) #meta score

m_votes = int(movie_blocks[0].find('span',{'name':'nv'}).get('data-value')) # votes

print("Movie Name: " + mname,
      "\nRelease Year: " + str(m_reyear),
      "\nIMDb Rating: " + str(m_rating),
      "\nMeta score: " + str(m_mscore),
      "\nVotes: " + '{:,}'.format(m_votes)

)
