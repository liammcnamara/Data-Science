# Stripping Tables from Websites using R


### Package

The simpliest package to use that will provide all the functionality needed is *rvest*.

You can read a detailed package describe [here](https://cran.r-project.org/web/packages/rvest/rvest.pdf).

Import the *rvest* library using:
```
library("rvest") 
```
### Step 1: URL
Declare a URL where the table of information is:

```
url <- "..... URL here ....."
```

### Step 2: Retrieve data
In *rvest* package, there is a function *read_html(.....)* which will retreive the raw HTML source from the *url* defined previously.

Arguments taken by *read_html(x, ..., encoding, as_html)*:

- x: URL path
- encoding: Encoding used for document
- as_html: Parse XML as HTML

Simply use the following statement to retrieve the data from the defined URL:
```
html_raw <- read_html(url)
```

### Step 3:
In this step we need to isolate the required table information from the HTML retrieve in **Step 2**. This can be done using *html_nodes(....)* provided in *rvest* package.

Arguments taken by *html_nodes(x, css, path)*:
- x: raw data from *read_html* (*rvest* refers to this as a document)
- css or xpath: node to retrieve from within HTML source.
```
table_raw <- html_nodes(html_raw, xpath='//*[@id=".... XPATH ...."]')
```

### Step 4:
This step will parse the HTML into a *dataframe* making the data more usable in R.

Arguments taken by *html_table(x, header, trim, fill, dec)*:
- x: Node or document (retrieved in **Step 3**)
- header: (True/False) Use the first row for headers
- trim: Trim/Remove white spaces
- fill: Fill rows with NA where no data is present
- dec: Charater used to mark a decimal place (. or ,)

In this case, we only need to pass the node retrieved in **Step 3**. The following statement should retrieve the table data as a dataframe:
```
df_table <- html_table(table_raw)[[1]]
```
*Note: [[1]] is used to isolate the table data and ignore the meta data that is also retrieved and stored in other elements.*

### Advanced
Another way to complete this is "fewer" lines would use forward-piping %>%
```
df_table <- url %>%
  read_html() %>% 
  html_nodes(xpath='//*[@id="... XPATH ..."]') %>%
  html_table()
```
*Note: %>% is forward piping which passes the returned values forward as parameters in the next function.*
