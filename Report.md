# Impact of Venues on Property Pricing - Report
*This is a report on how the venues nearby a property affect on its price.*

## Introduction/Business Problem

Today, there are many real estate companies in the world. These companies look for the best opportunities to invest. Within these opportunities, we find projects that involve huge investments. The problem is focused on Santiago de Chile, where there was a social crisis just before the COVID-19 crisis. Economy in Chile is not quite stable, this is why real estate companies have to make sure to invest only in the most promising projects.

Given this context, it's important for real estate companies to know how the surroundings of a property affect on its price. This way, they can know where their investment will have the highest pay off. Also, if they know how much the presence of each type of venue affects the price, they could reach a better decision on where to build.

To better understand how this approach can help these companies look at the following example. We have location A and location B, both with apparently similar conditions. The difference between these locations are that one has a supermarket and a school nearby, while the other has a park and a gym nearby. So, we could say that all four of these venues are a good thing to have close to our home (lets assume that). But we don't know in which of these locations to invest. If we had a model that quantifies the value that each type of venue adds to a property we could decide between these two locations rather easily (considering that the rest of the factors are pretty much the same).

On the other hand, this is very useful if there is a plan for new venues to be constructed near an evaluated location. So the price of the given location is not yet affected by these. If we knew how much value is going to be added by them, we can estimate the value of our unbuilt properties adding the effect of the upcoming venues. This is indeed very useful information for our stakeholders (real estate companies).


## Data

To accomplish the goal of learning the different impacts a specific type of venue has on a property's price, we will be using the Foursquare API and a website that has a listing of all the properties listed from July 2019 to today (www.portalinmobiliario.cl). I have already made a scrapper that gets the information from this website, and I will be using only a ".csv" file that represents that websites information.

The ".csv" file has the following columns:

* **Tipo de Propiedad (string):** Weather the it is an apartment, storage, house, etc (all are apartments because of how I downloaded the file)  
* **Tipo de Publicacion (string):** What kind of listing it is, rent or sail (here all sail)  
* **Direccion (string):** Address of the listed property  
* **Numero de Piezas (float):** Number of bedrooms in listed property  
* **Numero de Banos(float):** Number of bathrooms in listed property  
* **M2 Utiles (float):** Useful square meters of property  
* **M2 Totales (float):** Total square meters of property  
* **Precio en Pesos (float):** Price in CLP  
* **Precio en UF (float):** Price in UF (unit that takes into account the devaluation of the CLP)  
* **Fecha de Publicacion (string):** Date of listing  
* **Fecha de Extraccion (string):** Date in which the information was extracted from the website  
* **Lat (float):** Latitude of property  
* **Lng (float):** Longitude of property  
* **Estacionamiento Incluido (bool):** If the property has parking then True, if not False  
* **Bodega (float):** Number of storage rooms offered with property    
* **Condicion (string):** If the property is new or used  
* **Codigo (int):** Unique code for every listing on website  

As of the foursquare information, requests will be made in order to fill in the type of venues that each of these properties listed have around them. So, using the API that foursquare provides, I will be using the "search" endpoint with the intent parameter set to "browse". This way, I will get all of the venues in the given radius. This will return the following response fields:  

* **id:** A unique string identifier for this venue.  
* **name:** The best known name for this venue.  
* **location:** An object containing none, some, or all of address (street address), crossStreet, city, state, postalCode, country, lat, lng, and distance. All fields are strings, except for lat, lng, and distance. Distance is measured in meters. Some venues have their locations intentionally hidden for privacy reasons (such as private residences). If this is the case, the parameter isFuzzed will be set to true, and the lat/lng parameters will have reduced precision.  
* **categories:** An array, possibly empty, of categories that have been applied to this venue. One of the categories will have a primary field indicating that it is the primary category for the venue. For the complete category tree, see categories.  

Finally, I will merge the information given from the API with every property to which it corresponds. I will be only using the categories section from the foursquare response. As for the *csv* file I will use the price in CLP and the useful square meters fields. This way I will have the dependent variables, which are the different categories tow which a property is nearby. As well as the independent variable, which is the price per useful square meter.

***The actual dependent variables to be used are yet to be discovered, as this depends upon the correlation values of each type (category) with the price per square meter.***
