Singleton pattern
-----------------
The Singleton pattern addresses the problem of controlling object creation, ensuring that only one instance of a class exists in an application. This is particularly useful when a single object is required to coordinate actions across the system. For example, if you have a logger system, a configuration file, or a connection to a database, you might want to ensure that there's only one instance created.

Understand the Problem:
---------------------
A music player application should only have one player running at a time. If you attempt to open a new player while one is currently active, instead of starting a new player, it should only bring the existing one to the foreground.

Why This is a Problem?
---------------------
If our program doesn't handle these requests properly, every time we click the "play" button, it might start a new player instead of using the active player. This could lead to having multiple players running at the same time, playing different songs and causing a chaotic user experience.

How the Singleton Pattern will solve the problem?
----------------------
We can solve this problem using the Singleton design pattern, which ensures that a class has only one instance, and provides a global point of access to that instance. Think of the Singleton pattern like having only one stage on which our music player can perform.


Singelton structure in Python:
---
```
class SingletonMeta(type):
    _instances = {}
    
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]


class Singleton(metaclass=SingletonMeta):
    pass
}
```

Solution of player problem:
----
```
class Singleton:
    def __new__(cls, *args, **kwargs):
        if not hasattr(cls, 'instance'):
            cls.instance = super(Singleton, cls).__new__(cls)
        return cls.instance

class MusicPlayer(Singleton):
    pass

player1 = MusicPlayer()
player2 = MusicPlayer()

print(player1 is player2)  # outputs: True
```
