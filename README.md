# Exoplanet Existence
A machine learning model utilizing node regression to predict the existence of undiscovered exoplanets.


## Table of Contents
[Background](https://github.com/seanrhughes/exoplanet-existence#background)<br>

[Overview](https://github.com/seanrhughes/exoplanet-existence#overview)<br>

[Node Regression](https://github.com/seanrhughes/exoplanet-existence#node-regression)<br>
- [Node Properties](https://github.com/seanrhughes/exoplanet-existence#node-properties)<br>

[Results](https://github.com/seanrhughes/exoplanet-existence#results)<br>

[Predicting the Existence of Undiscovered Exoplanets](https://github.com/seanrhughes/exoplanet-existence#predicting-the-existence-of-undiscovered-exoplanets)<br>

## Background
Exoplanet detection is a critical aspect of modern astronomy / astrophysics. Currently, there are around 5500 confirmed exoplanets, and around 7000 candidate exoplanets.
The main method used to discover exoplanets is via transit of the planet across the star, however this occurence is extremely unlikely, as it requires the orbital plane
of the planetary system to be nearly edge-on as observed by telescopes in the solar system. Furthermore, the transit of a planet across a star takes a very small 
fraction of time compared to the period of the planet. Consequently, even if an eligible planetary system is being observered, it is unlikely a transit will be detected, let alone 
multiple transits at regular intervals, which is required to deduce exoplanet existence. Although transit accounts for the large majority of exoplanet discoveries,
these limiations result in nearly all exoplanets in surrounding planetary systems to go undiscovered. This project aims to predict the existence, and if so the number,
of exoplanets in those systems.


## Overview
This project was developed using `Python`, and uses `Neo4j` to create a graph in order to test and train a machine learning model using `node regression`.
The data for this project was parsed from [NASA's Exoplanet Archive](https://exoplanetarchive.ipac.caltech.edu).


## Node Regression 
Node regression is a machine learning technique applied to graphs that allows for the numerical prediction of node properties, based on other properties. In our case, 
the target property to be predicted on by the model is the number of exoplanets. The data parsed from the Exoplanet Archive is first compiled into nodes in a graph labeled by
stellar name, with stellar attributes stored as node properties. The general assumption made is that planetary systems with similar stellar attributes
will have a similar number of orbiting planets. For example, two planetary systems with relatively small stars should share more similar planetary structures than two systems
with wildly differing stellar mass. <br>
The node properties taken into account to make predictions during the regression are as follows: <br>

### Node Properties
<table>
  <tr>
    <th>Target Property</th>
  </tr>
  <tr>
    <td><code>Number of Planets</code></td>
  </tr>
</table>
<table>
  <tr>
    <th>Applied for Regression</th>
  </tr>
  <tr>
    <td><code>Stellar Mass</code></td>
  </tr>
  <tr>
    <td><code>Stellar Radius</code></td>
  </tr>
  <tr>
    <td><code>Stellar Age</code></td>
  </tr>
  <tr>
    <td><code>Stellar Metallicity</code></td>
  </tr>
  <tr>
    <td><code>Stellar Luminosity</code></td>
  </tr>
  <tr>
    <td><code>Stellar Density</code></td>
  </tr>
  <tr>
    <td><code>Stellar Effective Temperature</code></td>
  </tr>
  <tr>
    <td><code>Stellar Surface Gravity</code></td>
  </tr>
  <tr>
    <td><code>Stellar Rotational Velocity</code></td>
  </tr>
  <tr>
    <td><code>Stellar Rotational Period</code></td>
  </tr>
</table>

## Results
After the model is trained, we get a `Mean Squared Error` test score of `0.65`, and a `Mean Absolute Error` test score of `0.44`. This means:<br><br>

***On average, the model's error is less than a half of a planet per prediction.***<br><br>

For example, while testing on stars with known planets, the model correctly predicts many systems, including:

<table>
  <tr>
    <th>Stellar Name</th>
    <th>Number of Planets</th>
  </tr>
  <tr>
    <td>
       <a href="https://exoplanets.nasa.gov/exoplanet-catalog/1448/kepler-122-b/">Kepler-122</a>
    </td>
    <td>Five</td>
  </tr>
  <tr>
    <td>
       <a href="https://exoplanets.nasa.gov/exoplanet-catalog/1164/kepler-208-b/">Kepler-208</a>
    </td>
    <td>Four</td>
  </tr>
  <tr>
    <td>
       <a href="https://exoplanets.nasa.gov/exoplanet-catalog/4673/wasp-129-b/">WASP-129</a>
    </td>
    <td>One</td>
  </tr>
</table>

<br>
Where this model's results really become interesting, is when we use it to predict the existence of exoplanets where their discoveries have not been made:

## Predicting the Existence of Undiscovered Exoplanets

Let's take an example star, say Arcturus, a star very visible to the naked eye. This star is a relatively old red giant, and
the existence of any exoplanets orbiting Arcturus is currently unknown.<br><br>
If we enter Arcturus into the model, we get:

<table>
  <tr>
    <th>Stellar Name</th>
    <th>Number of Planets</th>
  </tr>
  <tr>
    <td>
      <a href="https://en.wikipedia.org/wiki/Arcturus">Arcturus</a>
    </td>
    <td>Four</td>
  </tr>
</table>

The model predicts Arcturus to have four exoplanets!<br><br>

We can continue these preditions with other stars having no known exoplanets: 

<table>
  <tr>
    <th>Stellar Name</th>
    <th>Number of Planets</th>
  </tr>
  
  <tr>
    <td>
      <a href="https://en.wikipedia.org/wiki/Aldebaran">Alderbaran</a>
    </td>
    <td>Four</td>
  </tr>

  <tr>
    <td>
      <a href="https://en.wikipedia.org/wiki/Regulus">Regulus</a>
    </td>
    <td>Three</td>
  </tr>

  <tr>
    <td>
      <a href="https://en.wikipedia.org/wiki/Polaris">Polaris</a>
    </td>
    <td>One</td>
  </tr>
  
</table>
<br>
These predictions offer valuable insight into the likely planetary structures of star systems with no current exoplanet discoveries.

