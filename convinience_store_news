import pandas as pd
import bs4
import requests
import openpyxl

page = 1
title_list = []
date_list = []
author_list = []
tag_list = []
describe_list = []
while page <= 12:
    data = requests.get(f'https://www.thaismescenter.com/page/{str(page)}/?s=เซเว่น')
    soup = bs4.BeautifulSoup(data.text)
    for n in soup.find_all('div', {'class':'article-content clearfix'}):
        title_list.append(n.find('h1',{'class':'entry-title'}).find('a').text)
        date_list.append(n.find('time',{'class':'entry-date published'}).text)
        author_list.append(n.find('span',{'class':'author vcard'}).text)
        tag_list.append(n.find('div',{'class':'above-entry-meta'}).text)
        describe_list.append(n.find('div',{'class':'entry-content clearfix'}).find('p').text)
    page += 1
    print('complete page number: ',page)
table = pd.DataFrame([title_list, date_list, author_list, tag_list, describe_list]).transpose()
table.columns = ['title','date','author','tag','describe']
table.set_index('title')
