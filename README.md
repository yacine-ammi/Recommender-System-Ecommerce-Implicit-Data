# Recommender System for Implicit Ecommerce Data
## Purpos of the study:
<p>
  The purpose of this project is to build a recommender system using implicit data from a multi category ecommerce store.<br>
  The dataset consists of two months's (Oct & Nov) behavioural clickstream data collected from the store's website, it is provided in seprate Excel spreadsheets for each month.<br>
  The total number of rows of the combined sheets is 109,950,743 row, each row in the file represents an event, all events are related to products and users, each event is like many-to-many relation between products and users.<p>
  
 ## The Dataset Structure:
    
<table>
<thead>
<tr>
<th>Property</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>event_time</strong></td>
<td>Time when event happened at (in UTC).</td>
</tr>
<tr>
<td><strong>event_type</strong></td>
<td>Three kinds of events: view, cart and purchase.</td>
</tr>
<tr>
<td><strong>product_id</strong></td>
<td>ID of a product</td>
</tr>
<tr>
<td><strong>category_id</strong></td>
<td>Product's category ID</td>
</tr>
<tr>
<td><strong>category_code</strong></td>
<td>Product's category taxonomy (code name) if it was possible to make it. Usually present for meaningful categories and skipped for different kinds of accessories.</td>
</tr>
<tr>
<td><strong>brand</strong></td>
<td>Downcased string of brand name. Can be missed.</td>
</tr>
<tr>
<td><strong>price</strong></td>
<td>Float price of a product. Present.</td>
</tr>
<tr>
<td><strong>user_id</strong></td>
<td>Permanent user ID.</td>
</tr>
<tr>
<td>** user_session**</td>
<td>Temporary user's session ID. Same for each user's session. Is changed every time user come back to online store from a long pause.</td>
</tr>
</tbody>
</table>

<p> The Event types are
<li><code>view</code> - a user viewed a product</li>
<li><code>cart</code> - a user added a product to shopping cart</li>
<li><code>purchase</code> - a user purchased a product</li></p>
 
<p>The approximate size of the dataset is <b>15GB</b>, it is hosted in Kaggle as "eCommerce behavior data from multi category store" and it can be accessed from <a href="https://www.kaggle.com/datasets/mkechinov/ecommerce-behavior-data-from-multi-category-store" target="_blank" rel="noopener noreferrer">here!</a>.<p>

## Methodology
<p>Due to the huge size of data, and limited amount of available resources of the kaggle kernels (16GB of RAM), the conventional methodes of reading, manipulating and anlysing data (mainly with Pandas DataFrame) could not be used in the preprocessing stage due to the folowing reasons:
<li>Pandas provides data structures for in-memory analytics. which makes using pandas to analyze datasets that are larger than memory datasets somewhat tricky.</li>
<li>Even datasets which are a sizable fraction of memory become unwieldy, as some pandas operations need to make intermediate copies.</li>
<li>Pandas lacks multiprocessing of tasks which makes complex tasks time consuming.</li></p>
 
To overcome these problems, other pwerfull libraries simillar to pandas were used in the first stages of this study (mainly preprocessing), we uesed the following libraries :
* **dask_cudf** : to load multiple files in parallel at the same time, and preprocess them without loading them to GPU memory.
* **cudf** : which is simillar to pandas, but it uses GPU memory and processor to speed up to calculations.
