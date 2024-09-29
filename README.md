import random
class Human:
    def __init__(self, name="Human", job = None, home = None, car = None):
        self.name = name
        self.money =100
        self.gladness = 50
        self.satiety = 50
        self.job = job
        self.car=car
        self.home=home

    def get_home(self):
        self.home = House()

    def get_car(self):
        self.car = Auto(brands_of_car)

    def get_job(self):
        if self.car.drive():
            pass
        else:
            self.to.repair()
            return
        self.job = Job(job_list)

    def eat(self):
        if self.home.food <=0:
            self.shopping("food")
        else:
            if self.satiety>=100:
                self.satiety=100
                return
            self.satiety +=5
            self.home.food -=5

    def work(self):
        if self.car.drive():
            pass
        else:
            if self.car.fuel<=20:
                self.shopping("fuel")
                return
            else:
                self.to_repair()
                return
            self.money += self.job.gladness_less
            self.gladness -= self.job.gladness_less
            self.satiety -= 4

    def shopping(self, manage):
        if self.car.drive():
            pass
        else:
            if self.car.fuel<=20:
                manage = "fuel"
            else:
                self.to_repair()
                return
            if manage == "fuel":
                print("Купую топливо")
                self.money -= 100
                self.car.fuel += 100
            elif manage == "food":
                print("Купую їжу")
                self.money -= 50
                self.home.food += 50
            elif manage == "delicious":
                print("Купую смаколики!!! Ура!!!")
                self.gladness += 10
                self.satiety += 2
                self.money -= 15

    def chill(self):
        self.gladness += 10
        self.home.mess +=5

    def clean_home(self):
        self.gladness -= 5
        self.home.mess = 0

    def to_repair(self):
        self.car.strength +=100
        self

    def days_indexes(self, day):
        day = f"Сьогодні {day} життя {self.name}"
        print(f"{day:=^50}", "\n")
        human_indexes = self.name + "індекси"
        print(f"{human_indexes:=^50}", "\n")
        print(f"Money - {self.money}")
        print(f"Satiety - {self.satiety}")
        print(f"Gladness - {self.gladness}")
        home_indexes = "Home indexes"
        print(f"{home_indexes:=^50}", "\n")
        print(f"Food - {self.home.food}")
        print(f"Mess - {self.home.mess}")
        car_indexes = f"{self.car.brand} car indexes"
        print(f"{car_indexes:=^50}", "\n")
        print(f"Fuel - {self.car.fuel}")
        print(f"Strength - {self.car.strength}")

    def is_alive(self):
        if self.gladness < 0:
            print("Depression...")
            return False
        if self.satiety < 0:
            print("Dead...")
            return False
        if self.money < -500:
            print("Bankrupt...")
            return False

    def live(self, day):
        if self.is_alive() == False:
            return False
        if self.home is None:
            print("Заселяємось в будинок")
            self.get_home()
        if self.car is None:
            self.get_car()
            print(f"Я купую мпшину {self.car.brand}")
        if self.job is None:
            self.get_job()
            print(f"Я шукаю роботу {self.job.job} із ЗП {self.job.salary}")
        self.days_indexes(day)
        dice = random.randint(1, 6)
        if self.satiety < 20:
            print("Іду їсти")
            self.eat()
        if self.gladness < 20:
            if self.home.mess > 15:
                print("Я хочу відпочити, але мені треба прибрати будинок")
                self.clean_home()
            else:
                print("Можна відпочити")
                self.chill()
        elif self.money <0:
            print("Start working")
            self.work()
        elif self.car.strength < 15:
            print("Я мушу ремонтувати автомобіль")
            self.to_repair()
        elif dice == 1:
            print("Lets chill")
            self.chill()
        elif dice == 2:
            print("Start working")
            self.work()
        elif dice == 3:
            print("Час уборки")
            self.clean_home()
        elif dice == 4:
            print("Час солодощів")
            self.shopping(manage="delicious")



class Auto:
    def __init__(self, brand_list):
        self.brand = random.choice(list(brand_list))
        self.fuel = brand_list[self.brand]["fuel"]
        self.strength = brand_list[self.brand]["strength"]
        self.consumption = brand_list[self.brand]["consumption"]

    def drive(self):
        if self.strength > 0 and self.fuel >= self.consumption:
            self.fuel -= self.consumption
            self.strength -= 1
            return True
        else:
            print("The car cannot move")
            return False

class House:
    def __init__(self):
        self.mess = 0
        self.food = 0

job_list = {
    "Java developer":
        {"salary": 50, "gladness_less": 10},
    "Python developer":
        {"salary": 40, "gladness_less": 3},
    "C++ developer":
        {"salary": 45, "gladness_less": 25},
    "Rust developer":
        {"salary": 70, "gladness_less": 1},
}
brands_of_car = {
    "BMW": {"fuel": 100, "strength": 100,
            "consumption": 6},
    "Lada": {"fuel": 50, "strength": 40,
            "consumption": 10},
    "Volvo": {"fuel": 70, "strength": 150,
        "consumption": 8},
    "Ferrari": {"fuel": 80, "strength": 120,
        "consumption": 14},
}

class Job:
    def __init__(self, job_list):
        self.job = random.choice(list(job_list))
        self.salary = job_list[self.job]["salary"]
        self.gladness_less = job_list[self.job]["gladness_less"]

Maksim = Human(name="Maksim")
for day in range(1, 8):
    if Maksim.live(day) == False:
        break
