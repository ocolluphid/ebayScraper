# eBay Sold Price Scraper

Note: This works as of the last commit. It's very likely some change in eBay's website will break this at some point after I stop maintaining.

This program is built to scrape all sold item data from eBay for any particular item. It will save the data to an excel file and create a scatter plot of the sold prices by date along with the median plot line and trendline. Further if you enter in the MSRP, it will plot a line for that and the break even prices of scalpers (particularly relevant when this was written during the PS5, Zen 3, and Xbox Series X launch). 

Examples:

![PS5 Example](https://github.com/driscoll42/ebayScraper/blob/master/Images/PS5.png)
![RTX 3080 Example](https://github.com/driscoll42/ebayScraper/blob/master/Images/RTX%203080.png)

# Install Instructions

* Create an Anaconda 3.8 python environment
* Run "pip install matplotlib==3.2.2, numpy, pandas==1.1.0, beautifulsoup==4.9.1, lxml==4.6.2, openpyxl==3.0.5, requests==2.25.0, scipy==1.5.4, xlrd==1.2.0, lxml, requests_cache
* Note: This code requires matplotlib 3.2.2, newer versions break the trend line

# How to Run
* In main.py update update the ebay_search() parameters for whatever product you are searching for as described below 
* Run main.py

# ebaysearch Parameters
- Search Parameters
  * query - Search you wish to perform on eBay, can include the following symbols ",", "(", ")", "-", and " " (Example: (AMD, Ryzen) 3100 -combo)
  * msrp - The MSRP of the product to estimate scalper profits, if not entered it will not display those lines
  * min_price - Default: 0 - The minimum price to search for
  * max_price - Default: 10000 - The maximum price to search for
  * sacat - Default: 0 - Can filter down to a specific category on eBay (For example, video game consoles = 139971) 
  * country - Default: USA - Allows for searching of different countries, currently only supports 'USA' and 'UK'
  * feedback - Default: False - Gets the seller feedback for each sold item. WARNING: This explodes run times as the code needs to call the url of every single item. In testing the 5950X extract with this false takes 8 seconds, with True it takes 40 minutes the first time. This is forced True if full_quantity is True as there is no extra work to get the feedback
  * quantity_hist - Default: False - Gets the full sold history of a multi-item listing. WARNING: This explodes run times
  * run_cached - Default: False - If True does not get new data from eBay, just runs the plots/analysis on the saved xlsx files. Most useful if want to get the data then run the plots using a different min date (e.g. for all time and then after post-launch only)
  * sleep_len - Default: 0.4 - How long to wait between url calls. This is to prevent DoSing eBay's servers and having your connection killed

* Filtering Parameters (Mostly to improve performance)
  * days_before - Default: 999 - How far back in time to search listings. Ends the search at current date - days_before. 


* Plotting/file Parameters
  * brand_list - Default: [] - If populated, will search for brands in the list in the title and populate a column with the brand found. This is case insensitive.
  * model_list - Default: [] - If populated, will search for brands in the list in the title and populate a column with the brand found. This is case insensitive.
  * min_date - Default: datetime.datetime(2020, 1, 1) - The earliest date to consider prices when plotting, useful if you want to split on preorders vs post-go live. Note that if you only have one day of data it errors out if you also have a msrp
  * extra_title_text - Default: '' - Extra text to add to the file name and plot titles 


* Debugging parameters
   * debug - Default: False - If True prints out exceptions. If verbose=True this is effectively True
   * verbose - Default: False - If True prints out all the data as soon as its pulled

## Release History

* 0.1.0
    * The first proper release
* 0.5.0
    * Added a number of performance enhancements and ensuring correct data being scraped