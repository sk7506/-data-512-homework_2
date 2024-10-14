# README

# Considering Bias in Data

## Project Goal
This homework explores the concept of bias in data using Wikipedia articles. It combines a dataset of Wikipedia articles with a dataset of country populations and uses a machine learning service called ORES to estimate the quality of each article.

Then, it analyzes  how the coverage of politicians on Wikipedia and the quality of articles about politicians varies among countries.

## Research Implications
### What (potential) sources of bias did you discover in the course of your data processing and analysis?
Data processing and analysis procedures lead to an inherent loss of information due to not every article title having a corresponding Revision ID, ORES Prediction, or other missing information. This missing information may underrepresent specific countries, affecting the results of the articles per capita and changing the total rankings. This is a reason for result variability among comparable analyses of the same data.

### What might your results suggest about (English) Wikipedia as a data source?
The following results over-represent politician coverage for countries with very low populations compared to politician coverage of high populations. This may be due to the metric 'per-capita' not being as robust a measurement as others used in demography and neighboring fields of study.

Furthermore, I notice high-income nations are over-represented in having high-quality articles, compared middle and low-income nations, with a skew towards low-population nations making the top 10 countries by high quality articles. High-quality Wikipedia articles are biased towards high-income, low-population countries.

### How might a researcher supplement or transform this dataset to potentially correct for the limitations/biases you observed?
One clear starting point is supplementing the source data with all politician articles, which would lessen the amount of countries with no match and raise the diversity of nations represented in the study. Another limitation was the inability of the ORES tool to find data on all politicians, raising questions about which nations are systemically under-represented in other analytical tools. This obstacle could be better handled by changing or updating the method used in generating the article quality predictions.

## Source Citation
The Wikipedia Category:Politicians by nationality was crawled to generate a list of Wikipedia article pages about politicians from a wide range of countries. This data is saved as **politicians_by_country.AUG.2024.csv**

The population data is available in CSV format as **population_by_country_AUG.2024.csv** This dataset was downloaded from the world population data sheet published by the Population Reference Bureau.

# Article Page Info MediaWiki API Example
This example illustrates how to access page info data using the [MediaWiki REST API for the EN Wikipedia](https://www.mediawiki.org/wiki/API:Main_page). This example shows how to request summary 'page info' for a single article page. The API documentation, [API:Info](https://www.mediawiki.org/wiki/API:Info), covers additional details that may be helpful when trying to use or understand this example.

## License
This code example was developed by Dr. David W. McDonald for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the [Creative Commons](https://creativecommons.org) [CC-BY license](https://creativecommons.org/licenses/by/4.0/). Revision 1.2 - September 16, 2024

# Requesting ORES scores through LiftWing ML Service API
Wikimedia Foundation (WMF) is reworking access to their APIs. It is likely in the coming years that all API access will require some kind of authentication, either through a simple key/token or through some version of OAuth. For now this is still a work in progress. You can follow the progress from their [API portal](https://api.wikimedia.org/wiki/Main_Page). Another on-going change is better control over API services in situations where those services require additional computational resources, beyond simply serving the text of a web page (i.e., the text of an article). Services like ORES that require running an ML model over the text of an article page is an example of a compute intensive API service.

Wikimedia is implementing a new Machine Learning (ML) service infrastructure that they call [LiftWing](https://wikitech.wikimedia.org/wiki/Machine_Learning/LiftWing). Given that ORES already has several ML models that have been well used, ORES is the first set of APIs that are being moved to LiftWing.

This example illustrates how to generate article quality estimates for article revisions using the LiftWing version of [ORES](https://www.mediawiki.org/wiki/ORES). The [ORES API documentation](https://ores.wikimedia.org) can be accessed from the main ORES page. The [ORES LiftWing documentation](https://wikitech.wikimedia.org/wiki/Machine_Learning/LiftWing/Usage) is very thin ... even thinner than the standard ORES documentation. Further, it is clear that some parameters have been renamed (e.g., "revid" in the old ORES API is now "rev_id" in the LiftWing ORES API).

## License
This code example was developed by Dr. David W. McDonald for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the [Creative Commons](https://creativecommons.org) [CC-BY license](https://creativecommons.org/licenses/by/4.0/). Revision 1.0 - August 15, 2023

## Intermediary and Final Data Files/Schema
### The following contextual files are either generated upon creation of the repository or loaded in/duplicated:

1.  **README.md** Created in R
2.  **LICENSE.txt**
3.  **__init__.py**
4.  **wp_pages_info_example.ipynb** Example source code provided via course materials
5.  **wp_ores_liftwing_example.ipynb** Example source code provided via course materials
6.  **politicians_by_country.AUG.2024.csv** Source data - politicians by country, taken from Wikipedia
7.  **population_by_country_AUG.2024.csv** Source data - world population data sheet published by the Population Reference Bureau.

### The following intermediary data files are generated by the scripts in this repository:
1. **failed_politicians_ORES_scores.json** output from the pages_info extractor with short list of politicians whose ORES predictions were not successful.
2. **high_quality_articles_by_country** intermediary file generated by the predictions notebook to confirm the code properly sums the amount of articles labeled 'FA' or 'GA', per country.
3. **politicians_by_country_no_ARTQUAL.csv** intermediary merged file without article quality scores
4. **politicians_final_ORES_scores.json** intermediary json file with full output from ORES tool
5. **politicians-and-revision-ids.json** intermediary python library output to a json file containing article names and revision IDs from the **data_extractor_for_ORES.ipynb**, which will be input into the ORES tool.
6. **wp_cleaned_analysis.csv** intermediary file with columns for country, region, population, number of articles, and number of high quality articles
7. **wp_cleaned_by_country** intermediary file of total and per-capita amount of articles and high quality articles per country
8. **wp_cleaned_by_region** intermediary file of total and per-capita amount of articles and high quality articles per region

### The following final data files are generated by the scripts in this repository:
1.  **data_extractor_for_ORES.ipynb** homework code referencing **wp_pages_info_example.ipynb**
2.  **wp_ores_liftwing_homework.ipynb** homework code referencing **wp_ores_liftwing_example.ipynb**
3. **wp_politicians_by_country** final csv file containing six columns: name, country, region, population, prediction, and revision ID
4. **wp_countries-no_match** final text file containing a list of countries from the **population_by_country_AUG.2024.csv** source data not included in the **politicians_by_country.AUG.2024.csv** source data

### Embedded Tables - Output of the Analysis
- Top 10 countries by coverage: The 10 countries with the highest total articles per capita (in descending order)
- Bottom 10 countries by coverage: The 10 countries with the lowest total articles per capita (in ascending order)
- Top 10 countries by high quality: The 10 countries with the highest high quality articles per capita (in descending order)
- Bottom 10 countries by high quality: The 10 countries with the lowest high quality articles per capita (in ascending order)
- Geographic regions by total coverage: A rank ordered list of geographic regions (in descending order) by total articles per capita.
- Geographic regions by high quality coverage: Rank ordered list of geographic regions (in descending order) by high quality articles per capita.

## Known Issues and Considerations
- Some articles may have limited data due to faulty information in the data collection process or in the data extraction process using the ORES tool
- Some countries from the source data are intentionally removed from the analysis due to having less than 1 million inhabitants
- Not all countries or politician Wikipedia articles were included in the source data
- Data quality may vary depending on the Wikipedia API's stored information.

## Reproducibility and Citation
This homework follows reproducible research practices. Portions of the code has been text-generated by ChatGPT, OpenAI, 14 Oct. 2024. These portions are noted in the markdown of the code preceding them, including the prompt, and are wrapped in a function to contain them. Note that all portions of text-generated code have been edited from their original versions for logic, clarity, and usability.

If you use this data or code, please provide proper credit to the Wikimedia Foundation as the source of the data, the ORES tool as the source of the predictions, and the example notebooks as the sources of the software.
