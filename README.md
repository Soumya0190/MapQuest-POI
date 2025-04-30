# MapQuest-POI
https://canvas.eee.uci.edu/courses/16697/assignments/334064


To break down the **MapQuest Project** using the **STAR** method (Situation, Task, Action, and Result):

### **Situation**:
You are tasked with creating a class called `MapQuest` that interfaces with the MapQuest OpenAPI. This API allows you to retrieve various location-based information, including distances, times, directions, and points of interest. Your goal is to use the MapQuest API to create a set of methods that can:
1. Calculate total distance for a series of locations.
2. Calculate the total time it takes to travel between those locations.
3. Generate a list of directions (turn-by-turn) between a sequence of locations.
4. Find points of interest near a location based on a keyword.

### **Task**:
You are required to implement a class with the following methods:
- `totalDistance`: Calculates the total distance for a list of locations, starting from the first and traveling in order.
- `totalTime`: Returns the total travel time for the list of locations.
- `directions`: Returns turn-by-turn driving directions between the locations.
- `pointOfInterest`: Finds nearby places of interest (e.g., restaurants, hotels) for a given location and keyword, returning a list of results.

### **Action**:
1. **Setup**:
   - You must first acquire a MapQuest API key and set up authentication.
   - Integrate the MapQuest Geocoding API to convert addresses to longitude and latitude, and the Directions API to calculate distances, times, and directions.

2. **Implement Methods**:
   - In the `totalDistance` method, you will send requests to the MapQuest Directions API, sequentially requesting the distance between each consecutive pair of locations in the list.
   - In the `totalTime` method, you will similarly calculate the time it takes to travel between the locations, again using the Directions API.
   - The `directions` method will return a string of turn-by-turn directions. You’ll need to format the API's responses into readable directions.
   - For the `pointOfInterest` method, you will send a request to the MapQuest Search API for nearby locations that match the keyword and return them in the specified format.

3. **Testing**:
   - Make sure to test each method with a variety of input cases to ensure robustness. For example, test empty lists, lists with one location, and lists with multiple locations.

### **Result**:
- **Correctness**: If implemented properly, the class should return accurate and meaningful information based on the MapQuest APIs. This includes the correct calculation of distance, time, directions, and points of interest.
- **Efficiency**: The project should handle different numbers of locations and edge cases (e.g., empty lists, large numbers of locations) efficiently.
- **Completion**: Once the methods are correctly implemented, you should be able to submit the Python script file according to the provided instructions for grading, and receive points for each method that works correctly during testing.

In summary, the project challenges you to integrate MapQuest APIs, handle geocoding, directions, and search for points of interest, while ensuring the correctness and functionality of the class through methodical testing.

---

#### **Usage Example**
```
api_key = "your_api_key_here"
mapquest = MapQuest(api_key)

locations = ["New York, NY", "Los Angeles, CA"]
print(mapquest.totalDistance(locations))  # Outputs the total distance

print(mapquest.totalTime(locations))  # Outputs the total time

print(mapquest.directions(locations))  # Outputs directions

poi = mapquest.pointOfInterest("New York, NY", "restaurant", 5)  # Finds nearby restaurants
print(poi)
```

---

This code defines a `MapQuest` class that interacts with the MapQuest API to calculate distances, travel times, directions, and points of interest between locations. Below is a breakdown of the functionality:

### Class Methods:

1. **`__init__(self, API_key)`**:
   - Initializes the class with an API key and sets a base URL for the MapQuest API route endpoint.

2. **`totalDistance(self, locations: list) -> float`**:
   - Calculates the total distance for a series of locations.
   - It loops through consecutive pairs of locations, making requests to the MapQuest API to get the distance between each pair.
   - If the list of locations has fewer than two entries, it returns 0.

3. **`totalTime(self, locations: list) -> int`**:
   - Calculates the total travel time for a series of locations.
   - Similar to `totalDistance`, it sums up the travel times between consecutive location pairs.
   - It also returns 0 if there are fewer than two locations.

4. **`directions(self, locations: list) -> str`**:
   - Provides step-by-step directions from the first location to the last.
   - It retrieves the narrative for each step in the route and returns them as a concatenated string.
   - If the list has fewer than two locations, it returns an empty string.

5. **`pointOfInterest(self, locations: str, keyword: str, results: int) -> list`**:
   - Searches for points of interest around a given location (`locations`), based on a keyword (e.g., "restaurants", "gas stations").
   - The results are sorted by distance and limited to the number specified (`results`).
   - It first geocodes the location into latitude and longitude and then queries the API for nearby points of interest based on that latitude/longitude.

### General Observations:
- **Error Handling**: The code lacks error handling for cases like invalid API responses, network issues, or incorrect inputs (e.g., if the MapQuest API rate limit is exceeded).
- **Optimization**: Each method makes a request to the MapQuest API for each pair of locations or point of interest. If the list is large, this could be inefficient. Consider using batching or optimizing the number of requests.
- **Validation**: It checks if `locations` has fewer than two entries but could be improved by validating the input more thoroughly (e.g., if locations are strings, etc.).

If you'd like to improve or modify any part of this code, such as adding error handling or optimizing the request logic, let me know!