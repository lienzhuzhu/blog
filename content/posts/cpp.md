+++
title = "C++ Library Set Up"
date = "2023-08-31T18:00:54-07:00"
# description = "Notes for setting up some libraries I use for C++ development"

tags = ["engineering"]
+++

### Eigen

```
git clone https://gitlab.com/libeigen/eigen.git ~/eigen
sudo ln -s ~/eigen/Eigen /usr/local/include/Eigen
```

Then test the installation by putting this code into a file called `eigen.cpp`:

```
#include <iostream>
#include <Eigen/Dense>
 
using Eigen::MatrixXd;
 
int main()
{
  MatrixXd m(2,2);
  m(0,0) = 3;
  m(1,0) = 2.5;
  m(0,1) = -1;
  m(1,1) = m(1,0) + m(0,1);
  std::cout << m << std::endl;
}
```


The following commands:

```
g++ eigen.cpp -o eigen-app
./eigen-app
```

should produce:

```
  3  -1
2.5 1.5
```


### SFML

```
brew install sfml
brew info sfml
```


From this output, we care about the path: `/opt/homebrew/Cellar/sfml/2.6.0/` as we will use this to establish symbolic links to the standard include and lib paths.

```
cd /opt/homebrew/Cellar/sfml/2.6.0/
sudo ln -s $(pwd)/include/SFML /usr/local/lib/SFML
cd /opt/homebrew/Cellar/sfml/2.6.0/lib
sudo ln -s $(pwd)/*.dylib /usr/local/lib/
```


Now we can test to make sure the library has been set up correctly. Put this code into a file called `sfml.cpp`.

```
#include <SFML/Graphics.hpp>

int main()
{
    sf::RenderWindow window(sf::VideoMode(200, 200), "SFML works!");
    sf::CircleShape shape(100.f);
    shape.setFillColor(sf::Color::Red);

    while (window.isOpen())
    {
        sf::Event event;
        while (window.pollEvent(event))
        {
            if (event.type == sf::Event::Closed)
                window.close();
        }

        window.clear();
        window.draw(shape);
        window.display();
    }

    return 0;
}
```

In whatever directory `sfml.cpp` is located, run the command:

```
g++ -o sfml-app sfml.cpp -lsfml-graphics -lsfml-window -lsfml-system
./sfml-app
```

and you should see a red circle show up on the screen.
