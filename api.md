
## 📍 **1. Introduction**

Google Places API is a web service that allows developers to **search**, **retrieve details**, and **display information** about places such as restaurants, hospitals, shops, landmarks, etc.
It is part of the Google Maps Platform.

Using Places API, you can:

* Search nearby places
* Perform text-based search
* Get complete details of any place
* Retrieve photos
* Implement autocomplete

---

## 🔑 **2. Getting an API Key**

To use the Places API:

1. Go to **Google Cloud Console**: [https://console.cloud.google.com](https://console.cloud.google.com)
2. Create a project
3. **Enable “Places API”**
4. Go to **APIs & Services → Credentials**
5. Create an **API Key**
6. Restrict your key to avoid misuse
7. Enable billing (required)

---

## 🧠 **3. API Endpoints Overview**

| Feature       | Endpoint                   |
| ------------- | -------------------------- |
| Nearby Search | `/place/nearbysearch/json` |
| Text Search   | `/place/textsearch/json`   |
| Place Details | `/place/details/json`      |
| Place Photos  | `/place/photo`             |
| Autocomplete  | `/place/autocomplete/json` |

---

# **4. Nearby Search**

Used to find places close to a location (lat/lng).

### ✅ **Syntax**

```
https://maps.googleapis.com/maps/api/place/nearbysearch/json
  ?location=LAT,LNG
  &radius=RADIUS_IN_METERS
  &type=PLACE_TYPE
  &key=YOUR_API_KEY
```

### 🔍 Example

```
https://maps.googleapis.com/maps/api/place/nearbysearch/json
?location=13.0827,80.2707
&radius=1500
&type=restaurant
&key=YOUR_API_KEY
```

---

# **5. Text Search**

Search by words like “cafes in Chennai”.

### ✅ Syntax

```
https://maps.googleapis.com/maps/api/place/textsearch/json
  ?query=YOUR_SEARCH_QUERY
  &key=YOUR_API_KEY
```

### 🔍 Example

```
https://maps.googleapis.com/maps/api/place/textsearch/json
  ?query=cafes+in+chennai
  &key=YOUR_API_KEY
```

---

# **6. Place Details**

Fetch detailed information using a **place_id**.

### ✅ Syntax

```
https://maps.googleapis.com/maps/api/place/details/json
  ?place_id=PLACE_ID
  &fields=FIELD1,FIELD2,FIELD3
  &key=YOUR_API_KEY
```

### 🔍 Example

```
https://maps.googleapis.com/maps/api/place/details/json
  ?place_id=ChIJJzj2p6RkUjoRj-FswTxiT9Q
  &fields=name,rating,formatted_address,formatted_phone_number,review
  &key=YOUR_API_KEY
```

---

# **7. Place Photos**

Download a photo using a `photo_reference`.

### ✅ Syntax

```
https://maps.googleapis.com/maps/api/place/photo
  ?maxwidth=400
  &photoreference=PHOTO_REF
  &key=YOUR_API_KEY
```

### 🔍 Example

```
https://maps.googleapis.com/maps/api/place/photo
  ?maxwidth=500
  &photoreference=AaYzUiRgGx8S5...
  &key=YOUR_API_KEY
```

---

# **8. Autocomplete (for search boxes)**

### ✅ Syntax

```
https://maps.googleapis.com/maps/api/place/autocomplete/json
  ?input=SEARCH_TEXT
  &key=YOUR_API_KEY
```

### 🔍 Example

```
https://maps.googleapis.com/maps/api/place/autocomplete/json
?input=starbucks
&key=YOUR_API_KEY
```

---

# **9. Example Using JavaScript (Fetch API)**

```javascript
const apiKey = "YOUR_API_KEY";
const url =
  `https://maps.googleapis.com/maps/api/place/nearbysearch/json?` +
  `location=13.0827,80.2707&radius=1500&type=restaurant&key=${apiKey}`;

fetch(url)
  .then(response => response.json())
  .then(data => {
    console.log("Nearby Places:", data.results);
  })
  .catch(error => console.error(error));
```

---

# **10. Example Using Python (Requests)**

```python
import requests

url = (
    "https://maps.googleapis.com/maps/api/place/textsearch/json?"
    "query=cafe+in+chennai&key=YOUR_API_KEY"
)

response = requests.get(url)
data = response.json()

print(data["results"])
```

---

# **11. Common Place Types**

```
restaurant
cafe
hospital
atm
school
bank
airport
shopping_mall
gym
movie_theater
```

Full list: [https://developers.google.com/maps/documentation/places/web-service/supported_types](https://developers.google.com/maps/documentation/places/web-service/supported_types)

---

# **12. Error Codes**

| Error              | Meaning                        |
| ------------------ | ------------------------------ |
| `REQUEST_DENIED`   | API key invalid or not enabled |
| `ZERO_RESULTS`     | No places found                |
| `OVER_QUERY_LIMIT` | Too many requests              |
| `INVALID_REQUEST`  | Missing parameters             |

---

# **13. Best Practices**

✔️ Restrict your API key
✔️ Cache responses to reduce cost
✔️ Request only needed fields (to reduce billing)
✔️ Handle quota errors

---

# **14. Conclusion**

Google Places API is powerful for building location-based apps. It allows searching, retrieving details, photos, reviews, and suggestions with simple HTTP requests.

