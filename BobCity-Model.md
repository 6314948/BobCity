classDiagram
    direction LR

    class Account {
      - decimal balance
      + decimal Balance()
      + void Deposit(decimal amount)
      + bool Withdraw(decimal amount)
    }

    class Job {
      + string Title
      + decimal HourlyRate
    }

    class IClock {
      <<interface>>
      + DateTime Now()
    }

    class SystemClock {
      + DateTime Now()
    }

    class TestClock {
      - DateTime _now
      + DateTime Now()
      + void Advance(TimeSpan delta)
    }

    class Animal {
      <<abstract>>
      + string Name
      + TimeSpan MinGapBetweenMeals
      + decimal MealCost
      + DateTime~nullable~ LastFedAt
      + string Speak()
      + bool IsHungry(DateTime now)
      + bool CanEat(DateTime now)
      + void Eat(DateTime now)
    }

    class Cat {
      + string Speak() "Miaou"
      + MinGapBetweenMeals = 10h
      + MealCost = 5
    }

    class Dog {
      + string Speak() "Wouff"
      + MinGapBetweenMeals = 8h
      + MealCost = 8
    }

    class Person {
      + string Name
      + Job Job
      + Account Account
      + List~Animal~ Pets
      + void Work(double hours, DateTime now)
      + bool Pay(decimal amount)
      + bool Feed(Animal pet, DateTime now)
      + int  FeedDue(DateTime now)
    }

    %% Relations
    Person "1" --> "1" Account : uses
    Person "1" --> "1" Job : has
    Person "1" --> "0..*" Animal : owns pets
    Animal <|-- Cat
    Animal <|-- Dog
    IClock <|.. SystemClock
    IClock <|.. TestClock
