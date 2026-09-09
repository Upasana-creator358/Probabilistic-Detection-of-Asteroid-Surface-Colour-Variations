# Data Processing

The purpose of processing is to compare the measured brightness with the brightness expected from a uniformly coloured asteroid.

## Main steps

1. Read the observation time, filter and brightness.
2. Correct the time for the light-travel delay from the asteroid to Earth.
3. Correct brightness for the changing asteroid-Sun and asteroid-observer distances.
4. Use the asteroid shape, rotation and phase function to predict its brightness.
5. Calculate the residual for every observation.
6. Calculate the Sun and observer directions in the asteroid's rotating frame.
7. Find the surface direction most strongly connected with the residual changes.
8. Measure this relationship separately in each filter.
9. Compare the filters using the Humes-Agarwal statistical test.

Monte Carlo tests are then used to repeat the analysis while changing uncertain inputs. This checks whether a result remains stable when realistic errors are included.
