```python
import re
from bs4 import BeautifulSoup
from tqdm import tqdm
import glob
import os
from time import sleep

import pandas as pd
from sec_edgar_downloader import Downloader
from near_regex import NEAR_regex
```


```python
sample_csv = "input/sp500_firms.csv"
if not os.path.exists(sample_csv):
    url = "https://en.wikipedia.org/wiki/List_of_S%26P_500_companies"
    sample = pd.read_html(url)[0]
    sample.to_csv(sample_csv, index=False)
else:
    sample = pd.read_csv(sample_csv)
```


```python
def extracto(fname):
 
    with open(fname, encoding="utf-8") as report_file:
        html = report_file.read()

    soup = BeautifulSoup(html,'lxml')

    for div in soup.find_all("div", {'style':'display:none'}): 
        div.decompose()

    lower = soup.text.lower()
    no_punc = re.sub(r'\W',' ',lower)
    cleaned = re.sub(r'\s+',' ',no_punc).strip()    
    
    return cleaned

```


```python
os.makedirs("Output", exist_ok=True)
```


```python
for index, row in sample[:25].iterrows():
    
    if(os.path.exists('10k_files/sec-edgar-filings/' + row['Symbol']) == True):
        num_folder = os.listdir('10k_files/sec-edgar-filings/' + row['Symbol'] + '/10-K')
        fname = '10k_files/sec-edgar-filings/' + row['Symbol'] + '/10-K/' + num_folder[0] + '/filing-details.html'
        with open(fname, encoding="utf-8") as report_file:
            html = report_file.read()
            macro_risk1 = len(re.findall(NEAR_regex(['(global|international|world)',
                                                     '(risk|risks)'],20),html))
            macro_risk2 = len(re.findall(NEAR_regex(['(political|economic|geopolitical)',
                                                     '(risk|risks)'],20),html))
            macro_risk3 = len(re.findall(NEAR_regex(['(tax|taxes|law|laws|policies|policy)',
                                                     '(risk|risks)'],20),html))
            macro_risk = macro_risk1 + macro_risk2 + macro_risk3
            
    if(os.path.exists('10k_files/sec-edgar-filings/' + row['Symbol']) == True):
        num_folder = os.listdir('10k_files/sec-edgar-filings/' + row['Symbol'] + '/10-K')
        fname = '10k_files/sec-edgar-filings/' + row['Symbol'] + '/10-K/' + num_folder[0] + '/filing-details.html'
        with open(fname, encoding="utf-8") as report_file:
            html = report_file.read()
            comp_risk1 = len(re.findall(NEAR_regex(['(competitive|competition)',
                                                     '(risk|risks|environment|change|changes)'],20),html))
            comp_risk2 = len(re.findall(NEAR_regex(['(customer service|pricing|product)',
                                                     '(risk|risks|change|changes)'],20),html))
            comp_risk3 = len(re.findall(NEAR_regex(['(innovative|innovate|disruptive|substitutions)',
                                                     '(risk|risks|change|changes)'],20),html))
            comp_risk = comp_risk1 + comp_risk2 + comp_risk3
            
    if(os.path.exists('10k_files/sec-edgar-filings/' + row['Symbol']) == True):
        num_folder = os.listdir('10k_files/sec-edgar-filings/' + row['Symbol'] + '/10-K')
        fname = '10k_files/sec-edgar-filings/' + row['Symbol'] + '/10-K/' + num_folder[0] + '/filing-details.html'
        #print(fname)
        with open(fname, encoding="utf-8") as report_file:
            html = report_file.read()
            supp_risk1 = len(re.findall(NEAR_regex(['(supply chain|supplier capacity)',
                                                     '(risk|risks|change|changes|shortages|constraints|adverse)'],20),html))
            supp_risk2 = len(re.findall(NEAR_regex(['(sourcing|raw material|production)',
                                                     '(risk|risks|change|changes|shortages|constraints|adverse)'],20),html))
            supp_risk3 = len(re.findall(NEAR_regex(['(fulfilling|price increases|price increase|manufacturers)',
                                                     '(risk|risks|change|changes|shortages|constraints|adverse)'],20),html))
            supp_risk = supp_risk1 + supp_risk2 + supp_risk3
    
    sample.at[index, 'Macro Risk']=macro_risk
    sample.at[index, 'Competitive Risk']=comp_risk
    sample.at[index, 'Supply Chain Risk']=supp_risk
    accounting_data = pd.read_stata('input/2019 ccm_cleaned (2).dta')
```


```python
new = sample.merge(accounting_data, how='outer', indicator='true', validate='1:m', right_on='tic', left_on='Symbol')
new_view = new[:25]
new_view
new_view.to_csv('Output/sp500_accting_plus_textrisks.csv')
```


```python
new_view
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Symbol</th>
      <th>Security</th>
      <th>SEC filings</th>
      <th>GICS Sector</th>
      <th>GICS Sub-Industry</th>
      <th>Headquarters Location</th>
      <th>Date first added</th>
      <th>CIK</th>
      <th>Founded</th>
      <th>Macro Risk</th>
      <th>...</th>
      <th>prof_a</th>
      <th>ppe_a</th>
      <th>cash_a</th>
      <th>xrd_a</th>
      <th>dltt_a</th>
      <th>invopps_FG09</th>
      <th>sales_g</th>
      <th>dv_a</th>
      <th>short_debt</th>
      <th>true</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>MMM</td>
      <td>3M</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Industrial Conglomerates</td>
      <td>Saint Paul, Minnesota</td>
      <td>1976-08-09</td>
      <td>66740.0</td>
      <td>1902</td>
      <td>10.0</td>
      <td>...</td>
      <td>0.193936</td>
      <td>0.228196</td>
      <td>0.065407</td>
      <td>0.042791</td>
      <td>0.408339</td>
      <td>2.749554</td>
      <td>NaN</td>
      <td>0.074252</td>
      <td>0.143810</td>
      <td>both</td>
    </tr>
    <tr>
      <th>1</th>
      <td>AOS</td>
      <td>A. O. Smith</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Building Products</td>
      <td>Milwaukee, Wisconsin</td>
      <td>2017-07-26</td>
      <td>91142.0</td>
      <td>1916</td>
      <td>5.0</td>
      <td>...</td>
      <td>0.177698</td>
      <td>0.193689</td>
      <td>0.180314</td>
      <td>0.028744</td>
      <td>0.103303</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.048790</td>
      <td>0.056170</td>
      <td>both</td>
    </tr>
    <tr>
      <th>2</th>
      <td>ABT</td>
      <td>Abbott</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>North Chicago, Illinois</td>
      <td>1964-03-31</td>
      <td>1800.0</td>
      <td>1888</td>
      <td>5.0</td>
      <td>...</td>
      <td>0.118653</td>
      <td>0.132161</td>
      <td>0.060984</td>
      <td>0.035942</td>
      <td>0.256544</td>
      <td>2.520681</td>
      <td>NaN</td>
      <td>0.033438</td>
      <td>0.088120</td>
      <td>both</td>
    </tr>
    <tr>
      <th>3</th>
      <td>ABBV</td>
      <td>AbbVie</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Pharmaceuticals</td>
      <td>North Chicago, Illinois</td>
      <td>2012-12-31</td>
      <td>1551152.0</td>
      <td>2013 (1888)</td>
      <td>4.0</td>
      <td>...</td>
      <td>0.178107</td>
      <td>0.037098</td>
      <td>0.448005</td>
      <td>0.076216</td>
      <td>0.709488</td>
      <td>2.211589</td>
      <td>NaN</td>
      <td>0.071436</td>
      <td>0.057566</td>
      <td>both</td>
    </tr>
    <tr>
      <th>4</th>
      <td>ABMD</td>
      <td>Abiomed</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>Danvers, Massachusetts</td>
      <td>2018-05-31</td>
      <td>815094.0</td>
      <td>1981</td>
      <td>5.0</td>
      <td>...</td>
      <td>0.225749</td>
      <td>0.137531</td>
      <td>0.466354</td>
      <td>0.088683</td>
      <td>0.000000</td>
      <td>12.164233</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>both</td>
    </tr>
    <tr>
      <th>5</th>
      <td>ACN</td>
      <td>Accenture</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>IT Consulting &amp; Other Services</td>
      <td>Dublin, Ireland</td>
      <td>2011-07-06</td>
      <td>1467373.0</td>
      <td>1989</td>
      <td>10.0</td>
      <td>...</td>
      <td>0.232395</td>
      <td>0.046699</td>
      <td>0.205780</td>
      <td>0.026846</td>
      <td>0.000545</td>
      <td>4.241083</td>
      <td>NaN</td>
      <td>0.062583</td>
      <td>0.282946</td>
      <td>both</td>
    </tr>
    <tr>
      <th>6</th>
      <td>ATVI</td>
      <td>Activision Blizzard</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Interactive Home Entertainment</td>
      <td>Santa Monica, California</td>
      <td>2015-08-31</td>
      <td>718877.0</td>
      <td>2008</td>
      <td>14.0</td>
      <td>...</td>
      <td>0.116553</td>
      <td>0.024439</td>
      <td>0.295440</td>
      <td>0.050290</td>
      <td>0.145377</td>
      <td>2.419659</td>
      <td>NaN</td>
      <td>0.014261</td>
      <td>0.021370</td>
      <td>both</td>
    </tr>
    <tr>
      <th>7</th>
      <td>ADM</td>
      <td>ADM</td>
      <td>reports</td>
      <td>Consumer Staples</td>
      <td>Agricultural Products</td>
      <td>Chicago, Illinois</td>
      <td>1981-07-29</td>
      <td>7084.0</td>
      <td>1902</td>
      <td>15.0</td>
      <td>...</td>
      <td>0.060527</td>
      <td>0.251767</td>
      <td>0.120690</td>
      <td>0.003500</td>
      <td>0.192127</td>
      <td>0.790464</td>
      <td>NaN</td>
      <td>0.017933</td>
      <td>0.144173</td>
      <td>both</td>
    </tr>
    <tr>
      <th>8</th>
      <td>ADBE</td>
      <td>Adobe</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Application Software</td>
      <td>San Jose, California</td>
      <td>1997-05-05</td>
      <td>796343.0</td>
      <td>1982</td>
      <td>8.0</td>
      <td>...</td>
      <td>0.185119</td>
      <td>0.062277</td>
      <td>0.201180</td>
      <td>0.092967</td>
      <td>0.047631</td>
      <td>7.442272</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0.761029</td>
      <td>both</td>
    </tr>
    <tr>
      <th>9</th>
      <td>ADP</td>
      <td>ADP</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Data Processing &amp; Outsourced Services</td>
      <td>Roseland, New Jersey</td>
      <td>1981-03-31</td>
      <td>8670.0</td>
      <td>1949</td>
      <td>5.0</td>
      <td>...</td>
      <td>0.083313</td>
      <td>0.018244</td>
      <td>0.046785</td>
      <td>0.015191</td>
      <td>0.047799</td>
      <td>1.755297</td>
      <td>NaN</td>
      <td>0.030868</td>
      <td>0.116689</td>
      <td>both</td>
    </tr>
    <tr>
      <th>10</th>
      <td>AAP</td>
      <td>Advance Auto Parts</td>
      <td>reports</td>
      <td>Consumer Discretionary</td>
      <td>Automotive Retail</td>
      <td>Raleigh, North Carolina</td>
      <td>2015-07-09</td>
      <td>1158449.0</td>
      <td>1932</td>
      <td>3.0</td>
      <td>...</td>
      <td>0.089422</td>
      <td>0.337692</td>
      <td>0.037220</td>
      <td>0.000000</td>
      <td>0.245764</td>
      <td>1.267617</td>
      <td>NaN</td>
      <td>0.001528</td>
      <td>0.147413</td>
      <td>both</td>
    </tr>
    <tr>
      <th>11</th>
      <td>AES</td>
      <td>AES</td>
      <td>reports</td>
      <td>Utilities</td>
      <td>Independent Power Producers &amp; Energy Traders</td>
      <td>Arlington, Virginia</td>
      <td>1998-10-02</td>
      <td>874761.0</td>
      <td>1981</td>
      <td>21.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>12</th>
      <td>AFL</td>
      <td>Aflac</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Life &amp; Health Insurance</td>
      <td>Columbus, Georgia</td>
      <td>1999-05-28</td>
      <td>4977.0</td>
      <td>1955</td>
      <td>25.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>13</th>
      <td>A</td>
      <td>Agilent Technologies</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>Santa Clara, California</td>
      <td>2000-06-05</td>
      <td>1090872.0</td>
      <td>1999</td>
      <td>0.0</td>
      <td>...</td>
      <td>0.134786</td>
      <td>0.089928</td>
      <td>0.146212</td>
      <td>0.042742</td>
      <td>0.189484</td>
      <td>2.767827</td>
      <td>NaN</td>
      <td>0.021794</td>
      <td>0.255920</td>
      <td>both</td>
    </tr>
    <tr>
      <th>14</th>
      <td>AIG</td>
      <td>AIG</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Property &amp; Casualty Insurance</td>
      <td>New York City, New York</td>
      <td>1980-03-31</td>
      <td>5272.0</td>
      <td>1919</td>
      <td>80.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>15</th>
      <td>APD</td>
      <td>Air Products</td>
      <td>reports</td>
      <td>Materials</td>
      <td>Industrial Gases</td>
      <td>Allentown, Pennsylvania</td>
      <td>1985-04-30</td>
      <td>2969.0</td>
      <td>1940</td>
      <td>14.0</td>
      <td>...</td>
      <td>0.169104</td>
      <td>0.545727</td>
      <td>0.127473</td>
      <td>0.003848</td>
      <td>0.170376</td>
      <td>2.713852</td>
      <td>NaN</td>
      <td>0.052474</td>
      <td>0.029645</td>
      <td>both</td>
    </tr>
    <tr>
      <th>16</th>
      <td>AKAM</td>
      <td>Akamai</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Internet Services &amp; Infrastructure</td>
      <td>Cambridge, Massachusetts</td>
      <td>2007-07-12</td>
      <td>1086222.0</td>
      <td>1998</td>
      <td>9.0</td>
      <td>...</td>
      <td>0.141254</td>
      <td>0.272675</td>
      <td>0.219355</td>
      <td>0.037301</td>
      <td>0.361355</td>
      <td>2.382912</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0.052205</td>
      <td>both</td>
    </tr>
    <tr>
      <th>17</th>
      <td>ALK</td>
      <td>Alaska Air Group</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Airlines</td>
      <td>Seattle, Washington</td>
      <td>2016-05-13</td>
      <td>766421.0</td>
      <td>1985</td>
      <td>9.0</td>
      <td>...</td>
      <td>0.117756</td>
      <td>0.662895</td>
      <td>0.117063</td>
      <td>0.000000</td>
      <td>0.208035</td>
      <td>0.834615</td>
      <td>NaN</td>
      <td>0.013315</td>
      <td>0.157156</td>
      <td>both</td>
    </tr>
    <tr>
      <th>18</th>
      <td>ALB</td>
      <td>Albemarle</td>
      <td>reports</td>
      <td>Materials</td>
      <td>Specialty Chemicals</td>
      <td>Charlotte, North Carolina</td>
      <td>2016-07-01</td>
      <td>915913.0</td>
      <td>1994</td>
      <td>12.0</td>
      <td>...</td>
      <td>0.098991</td>
      <td>0.511450</td>
      <td>0.062176</td>
      <td>0.005911</td>
      <td>0.301962</td>
      <td>1.067730</td>
      <td>NaN</td>
      <td>0.015435</td>
      <td>0.066019</td>
      <td>both</td>
    </tr>
    <tr>
      <th>19</th>
      <td>ARE</td>
      <td>Alexandria</td>
      <td>reports</td>
      <td>Real Estate</td>
      <td>Office REITs</td>
      <td>Pasadena, California</td>
      <td>2017-03-20</td>
      <td>1035443.0</td>
      <td>1994</td>
      <td>14.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>20</th>
      <td>ALGN</td>
      <td>Align</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Supplies</td>
      <td>San Jose, California</td>
      <td>2017-06-19</td>
      <td>1097149.0</td>
      <td>1997</td>
      <td>20.0</td>
      <td>...</td>
      <td>0.237323</td>
      <td>0.275112</td>
      <td>0.347353</td>
      <td>0.062927</td>
      <td>0.017380</td>
      <td>8.886138</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0.265828</td>
      <td>both</td>
    </tr>
    <tr>
      <th>21</th>
      <td>ALLE</td>
      <td>Allegion</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Building Products</td>
      <td>New York City, New York</td>
      <td>2013-12-02</td>
      <td>1579241.0</td>
      <td>1908</td>
      <td>11.0</td>
      <td>...</td>
      <td>0.219500</td>
      <td>0.125640</td>
      <td>0.120888</td>
      <td>0.018435</td>
      <td>0.499865</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.033904</td>
      <td>0.017163</td>
      <td>both</td>
    </tr>
    <tr>
      <th>22</th>
      <td>LNT</td>
      <td>Alliant Energy</td>
      <td>reports</td>
      <td>Utilities</td>
      <td>Electric Utilities</td>
      <td>Madison, Wisconsin</td>
      <td>2016-07-01</td>
      <td>352541.0</td>
      <td>1917</td>
      <td>10.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>23</th>
      <td>ALL</td>
      <td>Allstate</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Property &amp; Casualty Insurance</td>
      <td>Northfield Township, Illinois</td>
      <td>1995-07-13</td>
      <td>899051.0</td>
      <td>1931</td>
      <td>32.0</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
    </tr>
    <tr>
      <th>24</th>
      <td>GOOGL</td>
      <td>Alphabet (Class A)</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Interactive Media &amp; Services</td>
      <td>Mountain View, California</td>
      <td>2014-04-03</td>
      <td>1652044.0</td>
      <td>1998</td>
      <td>6.0</td>
      <td>...</td>
      <td>0.174452</td>
      <td>0.306576</td>
      <td>0.433748</td>
      <td>0.094299</td>
      <td>0.053525</td>
      <td>3.413887</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0.075092</td>
      <td>both</td>
    </tr>
  </tbody>
</table>
<p>25 rows × 52 columns</p>
</div>




```python

```
