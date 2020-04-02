# Impact of Venues on Property Pricing - Report
*This is a report on how the venues nearby a property affect on its price.*

## Introduction/Business Problem

Today, there are many real estate companies in the world. These companies look for the best opportunities to invest. Within these opportunities, we find projects that involve huge investments. The problem is focused on Santiago de Chile, where there was a social crisis just before the COVID-19 crisis. Economy in Chile is not quite stable, this is why real estate companies have to make sure to invest only in the most promising projects.

Given this context, it's important for real estate companies to know how the surroundings of a property affect on its price. This way, they can know where their investment will have the highest pay off. Also, if they know how much the presence of each type of venue affects the price, they could reach a better decision on where to build.

To better understand how this approach can help these companies look at the following example. We have location A and location B, both with apparently similar conditions. The difference between these locations are that one has a supermarket and a school nearby, while the other has a park and a gym nearby. So, we could say that all four of these venues are a good thing to have close to our home (lets assume that). But we don't know in which of these locations to invest. If we had a model that quantifies the value that each type of venue adds to a property we could decide between these two locations rather easily (considering that the rest of the factors are pretty much the same).

On the other hand, this is very useful if there is a plan for new venues to be constructed near an evaluated location. So the price of the given location is not yet affected by these. If we knew how much value is going to be added by them, we can estimate the value of our unbuilt properties adding the effect of the upcoming venues. This is indeed very useful information for our stakeholders (real estate companies).


## Data

To accomplish the goal of learning the different impacts that a specific type of venue has on a property's price, the Foursquare API and a website that has a listing of all the properties listed in Santiago de Chile from July 2019 to now (www.portalinmobiliario.cl) will be used. Scrapped data is already available in *.csv* format.

The *.csv* file has the following columns:

* **Tipo de Propiedad (string):** Wether the property is an apartment, storage, house, etc (all are apartments because of the downloaded info.)  
* **Tipo de Publicacion (string):** What kind of listing it is, rent or sale (here all are sale)  
* **Direccion (string):** Address of the listed property  
* **Numero de Piezas (float):** Number of bedrooms in listed property  
* **Numero de Banos(float):** Number of bathrooms in listed property  
* **M2 Utiles (float):** Useful square meters of property  
* **M2 Totales (float):** Total square meters of property  
* **Precio en Pesos (float):** Price in CLP  
* **Precio en UF (float):** Price in UF (unit that takes into account the devaluation of the CLP)  
* **Fecha de Publicacion (string):** Date of listing  
* **Fecha de Extraccion (string):** Date in which the information was extracted from the website  
* **Lat (float):** Latitude coordinate of property  
* **Lng (float):** Longitude coordinate of property  
* **Estacionamiento Incluido (bool):** If the property has parking then True, if not False  
* **Bodega (float):** Number of storage rooms offered with property    
* **Condicion (string):** If the property is new or used  
* **Codigo (int):** Unique code for every listing on website  

Regarding the Foursquare API, requests will be made in order to fill in the type of venues that each of these listed properties have around them. So, using the Foursquare's *search* endpoint with the *intent* parameter set to *browse* all of the venues in the given radius will be retrieved.

This will return the following response fields:  

* **id:** A unique string identifier for this venue.  
* **name:** The best known name for this venue.  
* **location:** An object containing none, some, or all of address (street address), crossStreet, city, state, postalCode, country, lat, lng, and distance. All fields are strings, except for lat, lng, and distance. Distance is measured in meters. Some venues have their locations intentionally hidden for privacy reasons (such as private residences). If this is the case, the parameter isFuzzed will be set to true, and the lat/lng parameters will have reduced precision.  
* **categories:** An array, possibly empty, of categories that have been applied to this venue. One of the categories will have a primary field indicating that it is the primary category for the venue. For the complete category tree, see categories.  

Finally, the information given from the API will be merged to every property to which it belongs. In the end, the only field that will be used from the Foursquare response is the categories section. As for the *.csv* file, the price in CLP and the useful square meters will be used (to retrieve the price per square meter). Then a model can be trained to predict how much each property's square meter is worth, depending on which types of venues are around it. In a regression model, the coefficients would represent the influence of the proximity of each type of venue on the final price of a property.
