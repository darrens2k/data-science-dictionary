# Dependent Data

Credits: ChatGPT

### What is it?

This refers to data in which observations are not independent from each other. Meaning that value of a single observation could have been influenced by the value of another observation.

There are different types of dependent data:

* Time Series Data: Each observation (or data point) is dependent on previous data points. For example, the weather of today may have been influenced by the weather of yesterday.

* Spatial Data: Observations (or data points) that are close to each other are more similar than data points which are further apart. Here the word "close" refers to distance measurement made using some distance metric, such as cosine distance. An example of this could be real estate prices in different neighbourhoods, the prices in a single neighbourhood should be more similar to each other than the prices of properties in different neighbourhoods.

* Hierarchical / Multi - Level Data: Observations (or data points) nested within higher level structures or within the same group are more similar to each other than observations in different groups. For example, all of the students in one school may be more similar to each other than students from different schools.

* Panel / Longitudinal Data: Within this type of data, observations are created for multiple subjects over multiple time periods. Thus there are groups of observations that are related across time. An example of this would be tracking the annual income of a group of people over several years.

### What do we use it for?

We can use dependent data to build powerful predictive models. Since data points are related, these relationships can be learnt and extrapolated, allowing for predictions to be made using these relationships.