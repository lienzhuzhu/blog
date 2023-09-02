+++
title = "C++ Library Set Up"
date = "2023-08-31T18:00:54-07:00"
# description = "Notes for setting up some libraries I use for C++ development"

tags = ["engineering"]
+++

### Eigen


### SFML

```
brew install sfml
brew info sfml
```


You should see some output similar to:

```
❯ brew info sfml
==> sfml: stable 2.6.0 (bottled), HEAD
Multi-media library with bindings for multiple languages
https://www.sfml-dev.org/
/opt/homebrew/Cellar/sfml/2.6.0 (806 files, 12.6MB) *
  Poured from bottle using the formulae.brew.sh API on 2023-08-28 at 09:23:09
From: https://github.com/Homebrew/homebrew-core/blob/HEAD/Formula/s/sfml.rb
License: Zlib
==> Dependencies
Build: cmake ✔, doxygen ✘
Required: flac ✔, freetype ✔, libogg ✔, libvorbis ✔
==> Options
--HEAD
        Install HEAD version
==> Analytics
install: 570 (30 days), 1,476 (90 days), 2,360 (365 days)
install-on-request: 525 (30 days), 1,365 (90 days), 2,209 (365 days)
build-error: 2 (30 days)
```


We care about the path: `/opt/homebrew/Cellar/sfml/2.6.0/` as we will use this to establish symbolic links to the standard include and lib paths.

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
