# Loading the Dataset #


```python
import pandas as pd
new_view = pd.read_csv('Output/sp500_accting_plus_textrisks.csv')
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
      <th>Unnamed: 0</th>
      <th>Symbol</th>
      <th>Security</th>
      <th>SEC filings</th>
      <th>GICS Sector</th>
      <th>GICS Sub-Industry</th>
      <th>Headquarters Location</th>
      <th>Date first added</th>
      <th>CIK</th>
      <th>Founded</th>
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
      <td>0</td>
      <td>MMM</td>
      <td>3M</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Industrial Conglomerates</td>
      <td>Saint Paul, Minnesota</td>
      <td>1976-08-09</td>
      <td>66740.0</td>
      <td>1902</td>
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
      <td>1</td>
      <td>AOS</td>
      <td>A. O. Smith</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Building Products</td>
      <td>Milwaukee, Wisconsin</td>
      <td>2017-07-26</td>
      <td>91142.0</td>
      <td>1916</td>
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
      <td>2</td>
      <td>ABT</td>
      <td>Abbott</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>North Chicago, Illinois</td>
      <td>1964-03-31</td>
      <td>1800.0</td>
      <td>1888</td>
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
      <td>3</td>
      <td>ABBV</td>
      <td>AbbVie</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Pharmaceuticals</td>
      <td>North Chicago, Illinois</td>
      <td>2012-12-31</td>
      <td>1551152.0</td>
      <td>2013 (1888)</td>
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
      <td>4</td>
      <td>ABMD</td>
      <td>Abiomed</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>Danvers, Massachusetts</td>
      <td>2018-05-31</td>
      <td>815094.0</td>
      <td>1981</td>
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
      <td>5</td>
      <td>ACN</td>
      <td>Accenture</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>IT Consulting &amp; Other Services</td>
      <td>Dublin, Ireland</td>
      <td>2011-07-06</td>
      <td>1467373.0</td>
      <td>1989</td>
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
      <td>6</td>
      <td>ATVI</td>
      <td>Activision Blizzard</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Interactive Home Entertainment</td>
      <td>Santa Monica, California</td>
      <td>2015-08-31</td>
      <td>718877.0</td>
      <td>2008</td>
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
      <td>7</td>
      <td>ADM</td>
      <td>ADM</td>
      <td>reports</td>
      <td>Consumer Staples</td>
      <td>Agricultural Products</td>
      <td>Chicago, Illinois</td>
      <td>1981-07-29</td>
      <td>7084.0</td>
      <td>1902</td>
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
      <td>8</td>
      <td>ADBE</td>
      <td>Adobe</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Application Software</td>
      <td>San Jose, California</td>
      <td>1997-05-05</td>
      <td>796343.0</td>
      <td>1982</td>
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
      <td>9</td>
      <td>ADP</td>
      <td>ADP</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Data Processing &amp; Outsourced Services</td>
      <td>Roseland, New Jersey</td>
      <td>1981-03-31</td>
      <td>8670.0</td>
      <td>1949</td>
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
      <td>10</td>
      <td>AAP</td>
      <td>Advance Auto Parts</td>
      <td>reports</td>
      <td>Consumer Discretionary</td>
      <td>Automotive Retail</td>
      <td>Raleigh, North Carolina</td>
      <td>2015-07-09</td>
      <td>1158449.0</td>
      <td>1932</td>
      <td>...</td>
      <td>0.089422</td>
      <td>0.337692</td>
      <td>0.037220</td>
      <td>0.000000</td>
      <td>0.245764</td>
      <td>1.267618</td>
      <td>NaN</td>
      <td>0.001528</td>
      <td>0.147413</td>
      <td>both</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>AES</td>
      <td>AES</td>
      <td>reports</td>
      <td>Utilities</td>
      <td>Independent Power Producers &amp; Energy Traders</td>
      <td>Arlington, Virginia</td>
      <td>1998-10-02</td>
      <td>874761.0</td>
      <td>1981</td>
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
      <td>12</td>
      <td>AFL</td>
      <td>Aflac</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Life &amp; Health Insurance</td>
      <td>Columbus, Georgia</td>
      <td>1999-05-28</td>
      <td>4977.0</td>
      <td>1955</td>
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
      <td>13</td>
      <td>A</td>
      <td>Agilent Technologies</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>Santa Clara, California</td>
      <td>2000-06-05</td>
      <td>1090872.0</td>
      <td>1999</td>
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
      <td>14</td>
      <td>AIG</td>
      <td>AIG</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Property &amp; Casualty Insurance</td>
      <td>New York City, New York</td>
      <td>1980-03-31</td>
      <td>5272.0</td>
      <td>1919</td>
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
      <td>15</td>
      <td>APD</td>
      <td>Air Products</td>
      <td>reports</td>
      <td>Materials</td>
      <td>Industrial Gases</td>
      <td>Allentown, Pennsylvania</td>
      <td>1985-04-30</td>
      <td>2969.0</td>
      <td>1940</td>
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
      <td>16</td>
      <td>AKAM</td>
      <td>Akamai</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Internet Services &amp; Infrastructure</td>
      <td>Cambridge, Massachusetts</td>
      <td>2007-07-12</td>
      <td>1086222.0</td>
      <td>1998</td>
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
      <td>17</td>
      <td>ALK</td>
      <td>Alaska Air Group</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Airlines</td>
      <td>Seattle, Washington</td>
      <td>2016-05-13</td>
      <td>766421.0</td>
      <td>1985</td>
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
      <td>18</td>
      <td>ALB</td>
      <td>Albemarle</td>
      <td>reports</td>
      <td>Materials</td>
      <td>Specialty Chemicals</td>
      <td>Charlotte, North Carolina</td>
      <td>2016-07-01</td>
      <td>915913.0</td>
      <td>1994</td>
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
      <td>19</td>
      <td>ARE</td>
      <td>Alexandria</td>
      <td>reports</td>
      <td>Real Estate</td>
      <td>Office REITs</td>
      <td>Pasadena, California</td>
      <td>2017-03-20</td>
      <td>1035443.0</td>
      <td>1994</td>
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
      <td>20</td>
      <td>ALGN</td>
      <td>Align</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Supplies</td>
      <td>San Jose, California</td>
      <td>2017-06-19</td>
      <td>1097149.0</td>
      <td>1997</td>
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
      <td>21</td>
      <td>ALLE</td>
      <td>Allegion</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Building Products</td>
      <td>New York City, New York</td>
      <td>2013-12-02</td>
      <td>1579241.0</td>
      <td>1908</td>
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
      <td>22</td>
      <td>LNT</td>
      <td>Alliant Energy</td>
      <td>reports</td>
      <td>Utilities</td>
      <td>Electric Utilities</td>
      <td>Madison, Wisconsin</td>
      <td>2016-07-01</td>
      <td>352541.0</td>
      <td>1917</td>
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
      <td>23</td>
      <td>ALL</td>
      <td>Allstate</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Property &amp; Casualty Insurance</td>
      <td>Northfield Township, Illinois</td>
      <td>1995-07-13</td>
      <td>899051.0</td>
      <td>1931</td>
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
      <td>24</td>
      <td>GOOGL</td>
      <td>Alphabet (Class A)</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Interactive Media &amp; Services</td>
      <td>Mountain View, California</td>
      <td>2014-04-03</td>
      <td>1652044.0</td>
      <td>1998</td>
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
<p>25 rows × 53 columns</p>
</div>



# Risk Measurement #

#### 1. Macro-Environment Risk ####

The Covid-19 Pandemic significantly affected the macro-environment outlook, both in the U.S. and abroad. Companies suddenly had to adapt to shifting policies both economic and political. If businesses were unable to aptly adapt to the everchanging macro-environment imposed on them, they would suffer as a result. Some companies had previously existing business models that were well suited for the constraints that Covid-19 placed on the economy,i.e. software/digital companies. While others, specifically brick and mortar retail, were impacted tremendously. Drilling down into specific key words that I believe to be a competent indicator of macro-environment risk, I decided to query each firms 10-K using the keywords attached in the code below. This would help indicate how much each firm percieved the shifting macro-environment as a risk. The relationship for this analysis being: frequency of keywords correlates to risk. I believe that keywords encompass macro-environment risk from a national and global level given that the national level would be apart of the larger global macro-enviroment. With a limit of 20 words in between, the function ensures that the words are mentioned within a vacinity that indicates a correlation is highly probable. While these factors have a quantitative impact on a company, they are wholly qualitative and are not measured in accounting data. 
macro_risk1 = len(re.findall(NEAR_regex(['(global|international|world)',
                                                     '(risk|risks)'],20),html))
macro_risk2 = len(re.findall(NEAR_regex(['(political|economic|geopolitical)',
                                                     '(risk|risks)'],20),html))
macro_risk3 = len(re.findall(NEAR_regex(['(tax|taxes|law|laws|policies|policy)',
                                                     '(risk|risks)'],20),html))
#### 2. Competitive Risk ####

In addition to the changing macro environment, companies also faced pressure from their competition. As previously mentioned, a given firms ability to adapt to the unique business climate that Covid-19 posed, would indicate their ability to perform successfully. Companies that competently executed this pivot would be ahead of the pack, and their stock returns should show this. I chose the keywords listed below because I believe that they serve as the best proxy for a firms competitive environment. I chose a wide variety of words ranging from the tangible (pricing, product, customer service) to the intangible (innovative, disruptive). I believed that this would help me identify the competitive risk as a whole. Both from a competitive pricing standpoint, and from new product competition. With a limit of 20 words in between, the function ensures that the words are mentioned within a vicinity that indicates a correlation is highly probable. While these factors have a quantitative impact on a company, they are wholly qualitative and are not measured in accounting data. 
comp_risk1 = len(re.findall(NEAR_regex(['(competitive|competition)',
                                                     '(risk|risks|environment|change|changes)'],20),html))
comp_risk2 = len(re.findall(NEAR_regex(['(customer service|pricing|product)',
                                                     '(risk|risks|change|changes)'],20),html))
comp_risk3 = len(re.findall(NEAR_regex(['(innovative|innovate|disruptive|substitutions)',
                                                     '(risk|risks|change|changes)'],20),html))
#### 3. Supply Chain Risk ####

Lastly, as a result of the Covid-19 pandemic, many industries experienced significant supply chain disruption. This was felt in a variety of separate areas. Whether it be manufacturer sourcing or raw material pricing, both business and consumer paid the price. Supply chain bottlenecks could also cause significant disruption to business that did not have diversified manufacturers. Over-exposure to a single manufacturer could have disastrous short and long term consequences for a company's performance. I chose these keywords because I hope to capture how many companies are dealing with supply chain issues/foresee supply chain risks moving forward. With a limit of 20 words in between, the function ensures that the words are mentioned within a vicinity that indicates a correlation is highly probable. While these factors have a quantitative impact on a company, they are wholly qualitative and are not measured in accounting data.  
supp_risk1 = len(re.findall(NEAR_regex(['(supply chain|supplier capacity)',                                             '(risk|risks|change|changes|shortages|constraints|adverse)'],20),html))
supp_risk2 = len(re.findall(NEAR_regex(['(sourcing|raw material|production)',                                                    '(risk|risks|change|changes|shortages|constraints|adverse)'],20),html))       supp_risk3 = len(re.findall(NEAR_regex(['(fulfilling|price increases|price increase|manufacturers)',                                           '(risk|risks|change|changes|shortages|constraints|adverse)'],20),html))
# Validation Check #

I believe these risk measures to be valid given their scope. They do not ecanpsulate an overwhelming amount of keywords. A factor that helps reduce incorrect hits that do not actually pertain to risk. At the same time, it is my belief that they contain enough words to get an accurate estimate of a companys exposure to that particular risk. Furthermore, through my sensitivity analysis, I deduced that 20 words was the ideal "max words between" when searching. This would, again, help to limit hits that do not actually pertain to risk while at the same time ensuring that their is a high probability of correlation. 

Disclaimer: given that my keyword search code is the same throughout the three risk measures, I will run a validation check on the supply chain risk code to ensure that it is working correctly. 

#### Correct Catch: Find ####


```python
import re
from near_regex import NEAR_regex
test = "I was looking at supply chain issues at large and noticed that supplier capacity is facing significant constraints."

supp_risk1 = len(re.findall(NEAR_regex(['(supply chain|supplier capacity)',
                                                     '(risk|risks|change|changes|shortages|constraints|adverse)'],20),test))
supp_risk2 = len(re.findall(NEAR_regex(['(sourcing|raw material|production)',
                                                     '(risk|risks|change|changes|shortages|constraints|adverse)'],20),test))
supp_risk3 = len(re.findall(NEAR_regex(['(fulfilling|price increases|price increase|manufacturers)',
                                                     '(risk|risks|change|changes|shortages|constraints|adverse)'],20),test))
supp_risk = supp_risk1 + supp_risk2 + supp_risk3
supp_risk
```




    1



#### Correct Catch: No find ####


```python
import re
from near_regex import NEAR_regex
test = "I was looking at supply chain issues at large and noticed that supplier capacity is facing significant issues."

supp_risk1 = len(re.findall(NEAR_regex(['(supply chain|supplier capacity)',
                                                     '(risk|risks|change|changes|shortages|constraints|adverse)'],20),test))
supp_risk2 = len(re.findall(NEAR_regex(['(sourcing|raw material|production)',
                                                     '(risk|risks|change|changes|shortages|constraints|adverse)'],20),test))
supp_risk3 = len(re.findall(NEAR_regex(['(fulfilling|price increases|price increase|manufacturers)',
                                                     '(risk|risks|change|changes|shortages|constraints|adverse)'],20),test))
supp_risk = supp_risk1 + supp_risk2 + supp_risk3
supp_risk
```




    0



# Final Sample Description #


```python
#risk_return_df.describe()
```

# Correlation Analysis #


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

import datetime
import matplotlib.pyplot as plt
import numpy as np
import pandas_datareader as pdr  
import seaborn as sns
from numpy.random import default_rng

sample_csv = "input/sp500_firms.csv"
if not os.path.exists(sample_csv):
    url = "https://en.wikipedia.org/wiki/List_of_S%26P_500_companies"
    sample = pd.read_html(url)[0]
    sample.to_csv(sample_csv, index=False)
else:
    sample = pd.read_csv(sample_csv)
    
new_view = pd.read_csv('Output/sp500_accting_plus_textrisks.csv')

return_data = pd.read_stata('input/2019-2020-stock_rets cleaned.dta')
return_data.rename(columns = {"ticker":"Symbol"}, inplace = True)
start_date = 20200309
end_date = 20200313

correct_dates = (return_data['date'] >= start_date) & (return_data['date'] <= end_date)
return_data = return_data.loc[correct_dates].set_index('date')
return_data['ret'] = pd.to_numeric(return_data['ret'])

return_data = (return_data.assign(weekly_return = 1 + return_data['ret']).groupby('Symbol')['weekly_return'].prod() - 1)
return_data = return_data.to_frame().reset_index()
risk_return_df = pd.merge(new_view, return_data, how = 'left', on = ['Symbol'], validate = 'many_to_many',indicator = True)
risk_return_df
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
      <th>Unnamed: 0</th>
      <th>Symbol</th>
      <th>Security</th>
      <th>SEC filings</th>
      <th>GICS Sector</th>
      <th>GICS Sub-Industry</th>
      <th>Headquarters Location</th>
      <th>Date first added</th>
      <th>CIK</th>
      <th>Founded</th>
      <th>...</th>
      <th>cash_a</th>
      <th>xrd_a</th>
      <th>dltt_a</th>
      <th>invopps_FG09</th>
      <th>sales_g</th>
      <th>dv_a</th>
      <th>short_debt</th>
      <th>true</th>
      <th>weekly_return</th>
      <th>_merge</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>MMM</td>
      <td>3M</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Industrial Conglomerates</td>
      <td>Saint Paul, Minnesota</td>
      <td>1976-08-09</td>
      <td>66740.0</td>
      <td>1902</td>
      <td>...</td>
      <td>0.065407</td>
      <td>0.042791</td>
      <td>0.408339</td>
      <td>2.749554</td>
      <td>NaN</td>
      <td>0.074252</td>
      <td>0.143810</td>
      <td>both</td>
      <td>-0.077905</td>
      <td>both</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>AOS</td>
      <td>A. O. Smith</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Building Products</td>
      <td>Milwaukee, Wisconsin</td>
      <td>2017-07-26</td>
      <td>91142.0</td>
      <td>1916</td>
      <td>...</td>
      <td>0.180314</td>
      <td>0.028744</td>
      <td>0.103303</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.048790</td>
      <td>0.056170</td>
      <td>both</td>
      <td>-0.028109</td>
      <td>both</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>ABT</td>
      <td>Abbott</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>North Chicago, Illinois</td>
      <td>1964-03-31</td>
      <td>1800.0</td>
      <td>1888</td>
      <td>...</td>
      <td>0.060984</td>
      <td>0.035942</td>
      <td>0.256544</td>
      <td>2.520681</td>
      <td>NaN</td>
      <td>0.033438</td>
      <td>0.088120</td>
      <td>both</td>
      <td>-0.001101</td>
      <td>both</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>ABBV</td>
      <td>AbbVie</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Pharmaceuticals</td>
      <td>North Chicago, Illinois</td>
      <td>2012-12-31</td>
      <td>1551152.0</td>
      <td>2013 (1888)</td>
      <td>...</td>
      <td>0.448005</td>
      <td>0.076216</td>
      <td>0.709488</td>
      <td>2.211589</td>
      <td>NaN</td>
      <td>0.071436</td>
      <td>0.057566</td>
      <td>both</td>
      <td>-0.038844</td>
      <td>both</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>ABMD</td>
      <td>Abiomed</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>Danvers, Massachusetts</td>
      <td>2018-05-31</td>
      <td>815094.0</td>
      <td>1981</td>
      <td>...</td>
      <td>0.466354</td>
      <td>0.088683</td>
      <td>0.000000</td>
      <td>12.164233</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>NaN</td>
      <td>both</td>
      <td>-0.090781</td>
      <td>both</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>ACN</td>
      <td>Accenture</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>IT Consulting &amp; Other Services</td>
      <td>Dublin, Ireland</td>
      <td>2011-07-06</td>
      <td>1467373.0</td>
      <td>1989</td>
      <td>...</td>
      <td>0.205780</td>
      <td>0.026846</td>
      <td>0.000545</td>
      <td>4.241083</td>
      <td>NaN</td>
      <td>0.062583</td>
      <td>0.282946</td>
      <td>both</td>
      <td>-0.068476</td>
      <td>both</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>ATVI</td>
      <td>Activision Blizzard</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Interactive Home Entertainment</td>
      <td>Santa Monica, California</td>
      <td>2015-08-31</td>
      <td>718877.0</td>
      <td>2008</td>
      <td>...</td>
      <td>0.295440</td>
      <td>0.050290</td>
      <td>0.145377</td>
      <td>2.419659</td>
      <td>NaN</td>
      <td>0.014261</td>
      <td>0.021370</td>
      <td>both</td>
      <td>-0.015509</td>
      <td>both</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>ADM</td>
      <td>ADM</td>
      <td>reports</td>
      <td>Consumer Staples</td>
      <td>Agricultural Products</td>
      <td>Chicago, Illinois</td>
      <td>1981-07-29</td>
      <td>7084.0</td>
      <td>1902</td>
      <td>...</td>
      <td>0.120690</td>
      <td>0.003500</td>
      <td>0.192127</td>
      <td>0.790464</td>
      <td>NaN</td>
      <td>0.017933</td>
      <td>0.144173</td>
      <td>both</td>
      <td>-0.079702</td>
      <td>both</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>ADBE</td>
      <td>Adobe</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Application Software</td>
      <td>San Jose, California</td>
      <td>1997-05-05</td>
      <td>796343.0</td>
      <td>1982</td>
      <td>...</td>
      <td>0.201180</td>
      <td>0.092967</td>
      <td>0.047631</td>
      <td>7.442272</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0.761029</td>
      <td>both</td>
      <td>-0.003772</td>
      <td>both</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>ADP</td>
      <td>ADP</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Data Processing &amp; Outsourced Services</td>
      <td>Roseland, New Jersey</td>
      <td>1981-03-31</td>
      <td>8670.0</td>
      <td>1949</td>
      <td>...</td>
      <td>0.046785</td>
      <td>0.015191</td>
      <td>0.047799</td>
      <td>1.755297</td>
      <td>NaN</td>
      <td>0.030868</td>
      <td>0.116689</td>
      <td>both</td>
      <td>-0.085709</td>
      <td>both</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>AAP</td>
      <td>Advance Auto Parts</td>
      <td>reports</td>
      <td>Consumer Discretionary</td>
      <td>Automotive Retail</td>
      <td>Raleigh, North Carolina</td>
      <td>2015-07-09</td>
      <td>1158449.0</td>
      <td>1932</td>
      <td>...</td>
      <td>0.037220</td>
      <td>0.000000</td>
      <td>0.245764</td>
      <td>1.267618</td>
      <td>NaN</td>
      <td>0.001528</td>
      <td>0.147413</td>
      <td>both</td>
      <td>-0.111173</td>
      <td>both</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>AES</td>
      <td>AES</td>
      <td>reports</td>
      <td>Utilities</td>
      <td>Independent Power Producers &amp; Energy Traders</td>
      <td>Arlington, Virginia</td>
      <td>1998-10-02</td>
      <td>874761.0</td>
      <td>1981</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
      <td>-0.227111</td>
      <td>both</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>AFL</td>
      <td>Aflac</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Life &amp; Health Insurance</td>
      <td>Columbus, Georgia</td>
      <td>1999-05-28</td>
      <td>4977.0</td>
      <td>1955</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
      <td>-0.149338</td>
      <td>both</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>A</td>
      <td>Agilent Technologies</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Equipment</td>
      <td>Santa Clara, California</td>
      <td>2000-06-05</td>
      <td>1090872.0</td>
      <td>1999</td>
      <td>...</td>
      <td>0.146212</td>
      <td>0.042742</td>
      <td>0.189484</td>
      <td>2.767827</td>
      <td>NaN</td>
      <td>0.021794</td>
      <td>0.255920</td>
      <td>both</td>
      <td>-0.119144</td>
      <td>both</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>AIG</td>
      <td>AIG</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Property &amp; Casualty Insurance</td>
      <td>New York City, New York</td>
      <td>1980-03-31</td>
      <td>5272.0</td>
      <td>1919</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
      <td>-0.238373</td>
      <td>both</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>APD</td>
      <td>Air Products</td>
      <td>reports</td>
      <td>Materials</td>
      <td>Industrial Gases</td>
      <td>Allentown, Pennsylvania</td>
      <td>1985-04-30</td>
      <td>2969.0</td>
      <td>1940</td>
      <td>...</td>
      <td>0.127473</td>
      <td>0.003848</td>
      <td>0.170376</td>
      <td>2.713852</td>
      <td>NaN</td>
      <td>0.052474</td>
      <td>0.029645</td>
      <td>both</td>
      <td>-0.101650</td>
      <td>both</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>AKAM</td>
      <td>Akamai</td>
      <td>reports</td>
      <td>Information Technology</td>
      <td>Internet Services &amp; Infrastructure</td>
      <td>Cambridge, Massachusetts</td>
      <td>2007-07-12</td>
      <td>1086222.0</td>
      <td>1998</td>
      <td>...</td>
      <td>0.219355</td>
      <td>0.037301</td>
      <td>0.361355</td>
      <td>2.382912</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0.052205</td>
      <td>both</td>
      <td>-0.053960</td>
      <td>both</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>ALK</td>
      <td>Alaska Air Group</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Airlines</td>
      <td>Seattle, Washington</td>
      <td>2016-05-13</td>
      <td>766421.0</td>
      <td>1985</td>
      <td>...</td>
      <td>0.117063</td>
      <td>0.000000</td>
      <td>0.208035</td>
      <td>0.834615</td>
      <td>NaN</td>
      <td>0.013315</td>
      <td>0.157156</td>
      <td>both</td>
      <td>-0.160584</td>
      <td>both</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>ALB</td>
      <td>Albemarle</td>
      <td>reports</td>
      <td>Materials</td>
      <td>Specialty Chemicals</td>
      <td>Charlotte, North Carolina</td>
      <td>2016-07-01</td>
      <td>915913.0</td>
      <td>1994</td>
      <td>...</td>
      <td>0.062176</td>
      <td>0.005911</td>
      <td>0.301962</td>
      <td>1.067730</td>
      <td>NaN</td>
      <td>0.015435</td>
      <td>0.066019</td>
      <td>both</td>
      <td>-0.171742</td>
      <td>both</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>ARE</td>
      <td>Alexandria</td>
      <td>reports</td>
      <td>Real Estate</td>
      <td>Office REITs</td>
      <td>Pasadena, California</td>
      <td>2017-03-20</td>
      <td>1035443.0</td>
      <td>1994</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
      <td>-0.071168</td>
      <td>both</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>ALGN</td>
      <td>Align</td>
      <td>reports</td>
      <td>Health Care</td>
      <td>Health Care Supplies</td>
      <td>San Jose, California</td>
      <td>2017-06-19</td>
      <td>1097149.0</td>
      <td>1997</td>
      <td>...</td>
      <td>0.347353</td>
      <td>0.062927</td>
      <td>0.017380</td>
      <td>8.886138</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0.265828</td>
      <td>both</td>
      <td>-0.130081</td>
      <td>both</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>ALLE</td>
      <td>Allegion</td>
      <td>reports</td>
      <td>Industrials</td>
      <td>Building Products</td>
      <td>New York City, New York</td>
      <td>2013-12-02</td>
      <td>1579241.0</td>
      <td>1908</td>
      <td>...</td>
      <td>0.120888</td>
      <td>0.018435</td>
      <td>0.499865</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>0.033904</td>
      <td>0.017163</td>
      <td>both</td>
      <td>-0.066694</td>
      <td>both</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22</td>
      <td>LNT</td>
      <td>Alliant Energy</td>
      <td>reports</td>
      <td>Utilities</td>
      <td>Electric Utilities</td>
      <td>Madison, Wisconsin</td>
      <td>2016-07-01</td>
      <td>352541.0</td>
      <td>1917</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
      <td>-0.114629</td>
      <td>both</td>
    </tr>
    <tr>
      <th>23</th>
      <td>23</td>
      <td>ALL</td>
      <td>Allstate</td>
      <td>reports</td>
      <td>Financials</td>
      <td>Property &amp; Casualty Insurance</td>
      <td>Northfield Township, Illinois</td>
      <td>1995-07-13</td>
      <td>899051.0</td>
      <td>1931</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>left_only</td>
      <td>-0.134124</td>
      <td>both</td>
    </tr>
    <tr>
      <th>24</th>
      <td>24</td>
      <td>GOOGL</td>
      <td>Alphabet (Class A)</td>
      <td>reports</td>
      <td>Communication Services</td>
      <td>Interactive Media &amp; Services</td>
      <td>Mountain View, California</td>
      <td>2014-04-03</td>
      <td>1652044.0</td>
      <td>1998</td>
      <td>...</td>
      <td>0.433748</td>
      <td>0.094299</td>
      <td>0.053525</td>
      <td>3.413887</td>
      <td>NaN</td>
      <td>0.000000</td>
      <td>0.075092</td>
      <td>both</td>
      <td>-0.062875</td>
      <td>both</td>
    </tr>
  </tbody>
</table>
<p>25 rows × 55 columns</p>
</div>




```python
ax = sns.lineplot(data = risk_return_df,
             x='Macro Risk',y='weekly_return')
plt.title("2020 Returns Week of 3/09")
plt.show()
```


    
![png](output_23_0.png)
    



```python
ax = sns.lineplot(data = risk_return_df,
             x='Competitive Risk',y='weekly_return')
plt.title("2020 Returns Week of 3/09")
plt.show()
```


    
![png](output_24_0.png)
    



```python
ax = sns.lineplot(data = risk_return_df,
             x='Supply Chain Risk',y='weekly_return') 
plt.title("2020 Returns Week of 3/09")
plt.show()
```


    
![png](output_25_0.png)
    


The graphs pictured above indicate that there is a relationship between Macro Risk and weekly returns, as well as Competitive Risk and weekly returns. In both instances there is a very noticeable decrease in the stock performance of companies that have higher risk numbers. This intuitively makes sense as greater risk usually carries a negative connotation for investors. With that said, the supply chain risk relationship was less correlated than the previous two. One reason I believe this to be the case is because supply chain issues hit virtually every industry. So while some may not have foreseen the risk ahead of time, they were impacted nevertheless. 


```python

```
