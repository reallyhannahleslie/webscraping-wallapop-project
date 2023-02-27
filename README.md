# webscraping-wallapop-project
A project looking at methods of using selenium to perform filtering and web scraping of the e-commerce site Wallapop

#### Objective: <br>
Wallapop is a Spanish second-hand resale site (similar to Gumtree or Facebook Marketplace) where users can sell items.
The goal of this project will be to scrape data from Wallapop in order to retrieve information of search results for different types of bicicyle results.

#### Criteria: <br>
- Initialize a Chrome web driver and access the Wallapop webpage
- Use the searchbox to look for all results matching the keyword “bicicleta” (bike in Spanish)
- Under the different search options provided, only access those entries in the category “Bicicletas” (bikes in Spanish)
- Filter the search results according to the following criteria:
    - 1. Location. Only retrieve results in “España, Barcelona” and narrow down the search to a maximum of “10km”
    - 2. Price. Limit the price to 800€.
    - 3. Subfield. Within the “Bicicletas” field, there are multiple subfields available. Include only results in the “Bicicletas y triciclos” subfield. 
    - 4. Labels. Retrieve only those results that correspond to “Bicicletas de carretera” (road bikes), “Bicicletas plegables” (foldable bikes) or “MTB” (mountain bikes).
    - 5. State. Only include those results that correspond to bikes that are “Nuevo” (New), “Como nuevo” (As good as new) and “En buen estado” (In good condition).
- Considering all the different combinations among the options above ("Bicicletas de carretera" and "Nuevo", "Bicicletas de carretera" and "En buen estado", etc.), retrieve the following information for all the available results (if less than 250) or for the first 250 results (if more than 250): Exclude all results corresponding to advertss.
    - The URL address to the post
    - The URL address to the displayed image
    - The title of the post
    - The price
    - The full description (as shown in the results page)
- Store the retrieved information in a DataFrame called df under the following columns:
    - "Link" (in str form)
    - “Title” (in str/object form)
    - “Description” (in str/object form)
    - “Price” (in float form)
    - “Image” (in str/object form).
    
#### Approach: <br>
Create a function for each stage of the scraping process before running them for each of the define subcategory combinations.
Get the list of filtering combinations for the type and state of the item and open a new browser to access the data.
For each browser opened:
* filter the data (general filters with a specific state-type combination)
* try scrolling till we reach the maximum number of allowed results or obtain all the items available from the filter applied
    * if we're not able to load new results in 3 minutes we stop scraping and collect the available data
* create a dataframe with data collected and clean the data, then aggregate for final answer
    
