# ![LOGO](logo.png) CORE API v2 **flow**ground Connector

## Description

A generated **flow**ground connector for the CORE API v2 API (version 2.0).

Generated from: https://api.apis.guru/v2/specs/core.ac.uk/2.0/swagger.json<br/>
Generated at: 2019-07-08T14:13:32+03:00

## API Description

<p style="text-align: justify;">You can use the CORE API to access the 
    resources harvested and enriched by CORE. If you encounter any problems with the API, please <a href="/contact">report them to us</a>.</p>

<h3>Overview</h3>
<p style="text-align: justify;">The API is organised by resource type. The resources are <b>articles</b>, 
    <b>journals</b> and <b>repositories</b> and are represented using JSON data format. Furthermore, 
    each resource has a list of methods. The API also provides two global methods for accessing all resources at once.</p>

<h3>Response format</h3>
<p style="text-align: justify;">Response for each query contains two fields: <b>status</b> and <b>data</b>.
    In case of an error status, the data field is empty. The data field contains a single object
    in case the request is for a specific identifier (e.g. CORE ID, CORE repository ID, etc.), or  
    contains a list of objects, for example for search queries. In case of batch requests, the response
    is an array of objects, each of which contains its own <b>status</b> and <b>data</b> fields.
    For search queries the response contains an additional field <b>totalHits</b>, which is the 
    total number of items which match the search criteria.</p>

<h3>Search query syntax</h3>

<p style="text-align: justify">Complex search queries can be used in all of the API search methods.
    The query can be a simple string or it can be built using terms and operators described in Elasticsearch
    <a href="http://www.elastic.co/guide/en/elasticsearch/reference/1.4/query-dsl-query-string-query.html#query-string-syntax">documentation</a>.
    The usable field names are <strong>title</strong>, <strong>description</strong>, <strong>fullText</strong>, 
    <strong>authors</strong>, <strong>publisher</strong>, <strong>repositories.id</strong>, <strong>repositories.name</strong>, 
    <strong>doi</strong>, <strong>oai</strong>, <strong>identifiers</strong> (which is a list of article identifiers including OAI, URL, etc.), <strong>language.name</strong> 
    and <strong>year</strong>. Some example queries:
</p>

<ul style="margin-left: 30px;">
    <li><p>title:psychology and language.name:English</p></li>
    <li><p>repositories.id:86 AND year:2014</p></li>
    <li><p>identifiers:"oai:aura.abdn.ac.uk:2164/3837" OR identifiers:"oai:aura.abdn.ac.uk:2164/3843"</p></li>
    <li><p>doi:"10.1186/1471-2458-6-309"</p></li>
</ul>

<h4>Retrieving the latest Articles</h4>
<p style="text-align: justify">
    You can retrieve the harvested items since specific dates using the following queries:
</p>

<ul style="margin-left: 30px;">
    <li><p>repositoryDocument.metadataUpdated:>2017-02-10</p></li>
    <li><p>repositoryDocument.metadataUpdated:>2017-03-01 AND repositoryDocument.metadataUpdated:<2017-03-31</p></li>    
</ul>

<h3>Sort order</h3>

<p style="text-align: justify;">For search queries, the results are ordered by relevance score. For batch 
    requests, the results are retrieved in the order of the requests.</p>

<h3>Parameters</h3>
<p style="text-align: justify;">The API methods allow different parameters to be passed. Additionally, there is an API key parameter which is common to all API methods. For all API methods 
    the API key can be provided either as a query parameter or in the request header. If the API key 
    is not provided, the API will return HTTP 401 error. You can register for an API key <a href="/services#api">here</a>.</p>

<h3>API methods</h3>

## Authorization

Supported authorization schemes:
- API Key
## Actions

### Get all near duplicate articles
> Method accepts values for several parameters and retrieves a JSON array of articles which have near duplicate content matching the input parameters' values. The response array contains ids of the near duplicate articles along with their relevance scores.<br/>

*Tags:* `articles`

#### Input Parameters
* `doi` - _optional_ - The DOI for which the duplicates will be identified<br/>
* `title` - _optional_ - Title to match when looking for duplicate articles. Only useful when either value for @year or @description is supplied.<br/>
* `year` - _optional_ - Year the article was published. Only useful when value for @title is supplied.<br/>
* `description` - _optional_ - Abstract for an article based on which its duplicates will be found. Only useful when value for @title is supplied.<br/>
* `fulltext` - _optional_ - Full text for an article based on which its duplicates will be found.<br/>
* `identifier` - _optional_ - Article identifier for which the duplicates will be identified. Only useful when either values for @doi or (@title and @year) or (@title and @abstract) or @fulltext are supplied.<br/>
* `repositoryId` - _optional_ - Limit the duplicates search to particular repository id.<br/>

### Batch operation for retrieving articles by CORE ID
> Method accepts a JSON array of CORE IDs and retrieves a list of articles. The response array is ordered based on the order of the IDs in the request array.<br/>

*Tags:* `articles`

#### Input Parameters
* `metadata` - _optional_ - Whether to retrieve the full article metadata or only the IDs. The default value is true<br/>
* `fulltext` - _optional_ - Whether to retrieve fulltexts of the articles. The default value is false<br/>
* `citations` - _optional_ - Whether to retrieve citations found in the articles. The default value is false<br/>
* `similar` - _optional_ - Whether to retrieve lists of similar articles. The default value is false. Because the similar articles are calculated on demand, setting this parameter to true might slightly slow down the response time<br/>
* `duplicate` - _optional_ - Whether to retrieve CORE IDs of different versions of the articles. The default value is false<br/>
* `urls` - _optional_ - Whether to retrieve lists of URLs of the article fulltexts. The default value is false<br/>
* `faithfulMetadata` - _optional_ - Returns the records raw XML metadata from the original repository. The default value is false<br/>

### Get article by CORE ID
> Method will retrieve an article based on given CORE ID.<br/>

*Tags:* `articles`

#### Input Parameters
* `coreId` - _required_ - CORE ID of the article that needs to be fetched.<br/>
* `metadata` - _optional_ - Whether to retrieve the full article metadata or only the ID. The default value is true.<br/>
* `fulltext` - _optional_ - Whether to retrieve full text of the article. The default value is false<br/>
* `citations` - _optional_ - Whether to retrieve citations found in the article. The default value is false<br/>
* `similar` - _optional_ - Whether to retrieve a list of similar articles. The default value is false. Because the similar articles are calculated on demand, setting this parameter to true might slightly slow down the response time<br/>
* `duplicate` - _optional_ - Whether to retrieve a list of CORE IDs of different versions of the article. The default value is false<br/>
* `urls` - _optional_ - Whether to retrieve a list of URLs from which the article can be downloaded. This can include links to PDFs as well as HTML pages. The default value is false<br/>
* `faithfulMetadata` - _optional_ - Returns the records raw XML metadata from the original repository. The default value is false<br/>

### Get fulltext PDF by CORE ID
> Method will retrieve an article based on given CORE ID.<br/>

*Tags:* `articles`

#### Input Parameters
* `coreId` - _required_ - ID of article history that needs to be fetched<br/>

### Get article history by CORE ID
> Method accepts a single CORE ID and returns a list of all historical versions of the article, which are stored in CORE database. The results are ordered from the newest one to the oldest one.<br/>

*Tags:* `articles`

#### Input Parameters
* `coreId` - _required_ - CORE ID of the article which history should be fetched<br/>
* `page` - _optional_ - Which page of the history results should be retrieved. Can be any number betwen 1 and 100, default is 1 (first page).<br/>
* `pageSize` - _optional_ - The number of results to return per page. Can be any number between 10 and 100, default is 10.<br/>

### Batch operation for search through articles
> Method accepts a JSON array of search queries and parameters. It then searches through all articles and returns a JSON array of search results for each of the queries. Method searches through all article fields (title, authors, subjects, identifiers, etc.).<br/>

*Tags:* `articles`

#### Input Parameters
* `metadata` - _optional_ - Whether to retrieve the full article metadata or only the ID. The default value is true.<br/>
* `fulltext` - _optional_ - Whether to retrieve full text of the article. The default value is false<br/>
* `citations` - _optional_ - Whether to retrieve citations found in the article. The default value is false<br/>
* `similar` - _optional_ - Whether to retrieve a list of similar articles. The default value is false. Because the similar articles are calculated on demand, setting this parameter to true might slightly slow down the response time<br/>
* `duplicate` - _optional_ - Whether to retrieve a list of CORE IDs of different versions of the article. The default value is false<br/>
* `urls` - _optional_ - Whether to retrieve a list of URLs from which the article can be downloaded. This can include links to PDFs as well as HTML pages. The default value is false<br/>
* `faithfulMetadata` - _optional_ - Whether to retrieve the raw XML metadata of the article. The default value is false<br/>

### Search through all documents
> Searches through all articles and returns a JSON array with search results. Method searches through all article fields.<br/>

*Tags:* `articles`

#### Input Parameters
* `query` - _required_ - The search query<br/>
* `page` - _optional_ - Which page of the search results should be retrieved. Can be any number betwen 1 and 100, default is 1 (first page).<br/>
* `pageSize` - _optional_ - The number of results to return per page. Can be any number between 10 and 100, default is 10.<br/>
* `metadata` - _optional_ - Whether to retrieve the full article metadata or only the ID. The default value is true.<br/>
* `fulltext` - _optional_ - Whether to retrieve full text of the article. The default value is false<br/>
* `citations` - _optional_ - Whether to retrieve citations found in the article. The default value is false<br/>
* `similar` - _optional_ - Whether to retrieve a list of similar articles. The default value is false. Because the similar articles are calculated on demand, setting this parameter to true might slightly slow down the response time<br/>
* `duplicate` - _optional_ - Whether to retrieve a list of CORE IDs of different versions of the article. The default value is false<br/>
* `urls` - _optional_ - Whether to retrieve a list of URLs from which the article can be downloaded. This can include links to PDFs as well as HTML pages. The default value is false<br/>
* `faithfulMetadata` - _optional_ - Returns the records raw XML metadata from the original repository. The default value is false<br/>

### Get articles by similarity to a text
> Method accepts a text and retrieves a JSON array of articles which are similar to the given text. The response array is ordered based on similarity score, starting from the most similar.<br/>

*Tags:* `articles`

#### Input Parameters
* `limit` - _optional_ - How many similar articles to retrieve at most. Can be any number betwen 1 and 100, default is 10<br/>
* `metadata` - _optional_ - Whether to retrieve the full article metadata or only the IDs of the similar articles. The default value is true<br/>
* `fulltext` - _optional_ - Whether to retrieve fulltexts of the similar articles. The default value is false<br/>
* `citations` - _optional_ - Whether to retrieve citations found in the articles. The default value is false<br/>
* `similar` - _optional_ - Whether to retrieve lists of similar articles. The default value is false. Because the similar articles are calculated on demand, setting this parameter to true might slightly slow down the response time<br/>
* `duplicate` - _optional_ - Whether to retrieve CORE IDs of different versions of the articles. The default value is false<br/>
* `urls` - _optional_ - Whether to retrieve lists of URLs of the article fulltexts. The default value is false<br/>
* `faithfulMetadata` - _optional_ - Whether to retrieve the raw XML metadata of the articles. The default value is false<br/>

### Batch operation for retrieving journals by ISSN
> Method accepts a JSON array of ISSNs and retrieves a list of journals.<br/>

*Tags:* `journals`

### Find journal by ISSN
> Returns a journal with given ISSN identifier.<br/>

*Tags:* `journals`

#### Input Parameters
* `issn` - _required_ - ISSN identifier of journal that needs to be fetched.<br/>

### Batch operation for search through journals
> Method accepts a JSON array of search queries and parameters. It then searches through all journals and returns a JSON array of search results for each of the queries. Method searches through all journal fields (title, identifiers, subjects, language, rights and publisher).<br/>

*Tags:* `journals`

### Search through journals
> Searches through all journals and returns a JSON array of search results. Method searches through all journal fields (title, identifiers, subjects, language, rights and publisher).<br/>

*Tags:* `journals`

#### Input Parameters
* `query` - _required_ - Search query<br/>
* `page` - _optional_ - Which page of the search results should be retrieved. Can be any number betwen 1 and 100, default is 1 (first page).<br/>
* `pageSize` - _optional_ - The number of results to return per page. Can be any number between 10 and 100, default is 10.<br/>

### Batch operation for retrieving repositories by CORE repository ID
> Method accepts a JSON array of CORE repository IDs and retrieves a list of repositories. The response array is ordered based on the order of the IDs in the request array. The maximum number of IDs in request is 100.<br/>

*Tags:* `repositories`

#### Input Parameters
* `stats` - _optional_ - Whether to retrieve statistics about the repository. The default value is false<br/>

### Get repository by CORE repository ID
> Method will retrieve a repository based on given CORE repository ID.<br/>

*Tags:* `repositories`

#### Input Parameters
* `repositoryId` - _required_ - CORE repository ID of the article that needs to be fetched.<br/>
* `stats` - _optional_ - Whether to retrieve statistics about the repository. The default value is false<br/>

### Batch operation for searching through repositories
> Method accepts a JSON array of search queries and parameters. It then searches through all repositories and returns a JSON array of search results for each of the queries. Method searches through all repository fields.<br/>

*Tags:* `repositories`

#### Input Parameters
* `stats` - _optional_ - Whether to retrieve statistics about the repository. The default value is false<br/>

### Search through all repositories
> Searches through all repositories and returns a JSON array with search results. Method searches through all repository fields.<br/>

*Tags:* `repositories`

#### Input Parameters
* `query` - _required_ - The search query<br/>
* `page` - _optional_ - Which page of the search results should be retrieved. Can be any number betwen 1 and 100, default is 1 (first page).<br/>
* `pageSize` - _optional_ - The number of results to return per page. Can be any number between 10 and 100, default is 10.<br/>
* `stats` - _optional_ - Whether to retrieve statistics about the repository. The default value is false<br/>

### Batch operation for search through all resources
> Method accepts a JSON array of search queries. It searches through all resources and returns a JSON array with search results for each of the queries. Method searches through all resources and all fields. The results are ordered by relevance score and contain type of the relevant resource and its ID. Furthermore, the responses are oredered based on the order of the request items. The metadata of each resource need to be obtained through an appropriate method.<br/>

*Tags:* `all`

### Search through all resources
> Searches through all resources and returns a JSON array with search results. Method searches through all resources and all fields. The results are ordered by relevance score and contain type of the relevant resource and its ID. The metadata of each resource need to be obtained through an appropriate method.<br/>

*Tags:* `all`

#### Input Parameters
* `query` - _required_ - The search query<br/>
* `page` - _optional_ - Which page of the search results should be retrieved. Can be any number betwen 1 and 100, default is 1 (first page).<br/>
* `pageSize` - _optional_ - The number of results to return per page. Can be any number between 10 and 100, default is 10.<br/>

## License

**flow**ground :- Telekom iPaaS / core-ac-uk-connector<br/>
Copyright © 2019, [Deutsche Telekom AG](https://www.telekom.de)<br/>
contact: flowground@telekom.de

All files of this connector are licensed under the Apache 2.0 License. For details
see the file LICENSE on the toplevel directory.
