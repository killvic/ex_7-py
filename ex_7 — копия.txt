class Date:
    day = month = year = ''

    def __str__(self):
        return f'{self.day},{self.month},{self.year}'


class Person:
    name = lastname = height = weight = ''
    dateOfBirth = None

    def __str__(self):
        return f'{self.name},{self.lastname},{self.dateOfBirth},{self.height},{self.weight}'


def print_list(filename, person_list):
    for element in person_list:
        print(element)
    with open(filename, "w") as output:
        for element in person_list:
            output.write(element.__str__() + '\n')
        output.close()


persons = []

with open("persons.txt", "r") as input_file:
    for person in input_file.readlines():
        buffer = person.split(",")

        bufferperson = Person()
        bufferperson.dateOfBirth = Date()
        bufferperson.name = buffer[0]
        bufferperson.lastname = buffer[1]
        bufferperson.dateOfBirth.day = buffer[2]
        bufferperson.dateOfBirth.month = buffer[3]
        bufferperson.dateOfBirth.year = buffer[4]
        bufferperson.height = buffer[5]
        bufferperson.weight = buffer[6][:-1]

        persons.append(bufferperson)

print("Input:")
for line in persons:
    print(line)

print("By first name:")
print_list("by_first_name.csv", sorted(persons, key=lambda x: x.name))

print("By last name:")
print_list("by_last_name.csv", sorted(persons, key=lambda x: x.lastname))

print("By date:")
print_list("by_date.csv", sorted(persons, key=lambda x: (x.dateOfBirth.year, x.dateOfBirth.month, x.dateOfBirth.day)))

print("By height:")
print_list("by_hieght.csv", sorted(persons, key=lambda x: x.height))

print("By weight:")
print_list("by_weight.csv", sorted(persons, key=lambda x: x.weight))

print("By bmi:")
print_list("by_bmi.csv", sorted(persons, key=lambda x: (float(x.weight) / ((int(x.height) / 100) * (int(x.height) / 100)))))
