Download either the compressed binary files for either [Windows]({{ site.baseurl}}/assets/binary/Magnus_Effect.zip) or 
[Linux]({{ site.baseurl}}/assets/binary/Magnus_Effect.tar), unzip the files, then run the "MagnusEffect" executable. 
The controls will be displayed in the GUI right away. 

# Drag coefficients

There are a number of preset drag coefficients that are togglable through the programs GUI. The defaults refer to those drag 
coefficients [empirically found to fit the experimental model](./comparison). The rest are coefficients by other more reputable 
authors, respectively:

![Coefficients](/assets/img/coefficients.png)

* [Cho-Leutheusser](https://open.library.ubc.ca/cIRcle/collections/undergraduateresearch/51869/items/1.0107239): for ping pong
* [Adair-Giordano](http://physics.wooster.edu/JrIS/Files/nowicki.pdf): for baseball
* [John Wesson](https://books.google.ca/books/about/The_Science_of_Soccer.html?id=dGc8rt8IYdwC): for soccer

# Statistical Analysis

In order to run the statistical analysis between the model and reality described [here](./comparison), make sure "Show automation" 
has been pressed. Star The subsequent window will allow you to "Start automation", which will begin simulating using the initial 
conditions of the experiments conducted. The current values for the [MAPD](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error) 
of the evaluated variables will update as the software iterates through them. "Time between iterations" is editable, and will determine 
how much time a simulation will last before moving on to the next experiment (iteration).

![Automation](/assets/img/automation-instructions.PNG)