# TechAcademyLiveProject (Python)
INTRODUCTION

For the last two weeks I participated in a live project at The Tech Academy. It involved a real world software development project. This project was a web scraping travel application that gathered data from the web that would be relevant to the user. It included weather, flight info, events, restaurants, etc. The main language used for this project was Python.

Here is a list of the technologies used in this project:
  Django Web Framework
  Selenium (Python library)
  BeautifulSoup (Python library)
  Virtualenv (Python library)
  VS Code (Code editor)
  Azure DevOps (Project management)
  Git (Source control)
  
I want to include the golden rules in my code summary just so I can review them again later when I go over this in the job placement course:
  GOLDEN RULES OF LIVE PROJECT

    1) DO NOT create a pull request if there are errors or bugs in the code
       This means no red squiggly lines, and it loads properly when run
    2) If you think there’s an error in your assignment, bring it up
       You will not have a perfect boss, double check it wasn’t a mistake
    3) Keep your local master branch updated! (reduce merge conflicts)
    If you are getting no new commits, make sure you’re on the master branch
    4) Comment your Code, Commit often, Test, Test, and Test again
    5) Questions are always preferred to radio silence
    6) Do not use escape characters (like \ ) when naming your branch
    7) Use the IDE we are working in, trying to switch back and forth will only confuse you
    8) Create new branches for each story, and commit changes before switching branches
    9) Creativity is encouraged! Show off those skills, especially front end
    10) Always try the simple solution first (aka The “Clear the Cache” Rule).



Working on this project was a great learning experience. Not only did I sharpen my coding skills but I had a chance to see how it will be like to work on a team of other developers. I also learned how to use Git, which was not a strong point in my learning career. It's certainly a vital part of being a software developer.

Below are descriptions of the stories I worked on along with code snippets.

  First story: We are getting reports from our users that they would like to be able to choose from a larger selection of photos than     the four we have currently.  Find some pics that relate in some way to travel and add them to our project so users can select them as   their background (about 10 total)-- hint a new one has already been uploaded, you'll just need to include it in the options.

This was good beginner story to work on for me. It allowed me the opportunity to become familiar with the project without being too overwhelming. I had to search around through the files quite a bit to find where the photo files were in the code. I also had to ask my team mates where things were because I didn't want to spend too much time searching. Once I found the file it was very straightforward from there. I downloaded some good quality, pixel-appropriate photos from the web and added them to the folder then put them in the code.

/********SCRIPTS FOR CHANGING BACKGROUND IMAGE**********/
$(userBackground);
var img = ["/static/images/traveling.jpg","/static/images/Airplane.jpg","/static/images/Beach.jpg","/static/images/Florence.jpg","/static/images/Map.jpg","/static/images/SouthKorea.jpg","/static/images/Globe.jpg","/static/images/Airplane2.jpg","/static/images/Japan.jpeg","/static/images/Iceland.jpg","/static/images/Beach2.jpg"];

  Second story: This will be a new app that we will use to scrape data from wikipedia using beautiful soup.  This app will display         information about the world that will be relevant to travelers.Eventually, we will use this app to display data scraped from multiple   wikipedia pages, but to begin this app, we will just have one section where we scrape data from this wikipedia article:

  https://en.wikipedia.org/wiki/List_of_countries_by_population_(United_Nations)

  Requirements:
  Use beautiful soup to pull data from this article including country name, country population, and region.
  Create a table that display this information.
  
 This story was a bit more challenging but I was up for it. I wanted a chance to do more coding now that I was familiar with the project. It was helpful to see code from the other applications so that I could keep my application looking similar and follow the style of the site. Web scraping was more difficult due to having to isolate the exact html elements you want from the site. I hit many roadblocks that included getting the info into a usable state once I had scraped it and figuring out which route to go as far as displaying it to the site. At first, I wanted to incorporate a "Load Data" button to click and it would show the data. That turned out to be an unneccessary challenge so I took a different route of converting my csv file to html form then putting that into the site. It worked perfectly and I'm so glad I took that route instead.
 
 Below is a snippet of the web scraping portion of the application.
 
 #web scraping code to get country or area, UN continental region, UN statistical region, 
# population (July 1, 2018), population (July 1, 2019), percent change in population
import requests #for getting content from a URL
from bs4 import BeautifulSoup #is used to parse through the HTML we get from requests
import pandas as pd 
import csv
import numpy as np
import re
from urllib.request import urlopen
from prettytable import PrettyTable

url = "https://en.wikipedia.org/wiki/List_of_countries_by_population_(United_Nations)"
html = urlopen(url)

soup = BeautifulSoup(html, "lxml")

title = soup.title
links = soup.find('a', href=True)

for link in links:
    data = []
    allrows = soup.find_all("tr")
    for row in allrows:
        row_list = row.find_all("td")
        dataRow = []
        for cell in row_list:
            dataRow.append(cell.text)
        data.append(dataRow)
data = data[1:]

df = pd.DataFrame(data)
df.to_csv('worldtable.csv', encoding='utf-8', index=False)
print(open('worldtable.csv','r').read()) 


