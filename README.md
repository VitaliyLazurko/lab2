# lab2
МІНІСТЕРСТВО ОСВІТИ І НАУКИ УКРАЇНИ

Національний аерокосмічний університет ім. М. Є. Жуковського «Харківський авіаційний інститут»

Факультет «Радіоелектроніки, комп’ютерних систем та інфокомунікацій» Кафедра «Аерокосмічних радіоелектронних систем»

Лабораторна робота №2

з дисципліни «Інформаційно-комунікаційні мережі »

на тему: «Основи роботи з Terraform»

Виконав: студент 4 курсу групи № 536-ст напряму підготовки (спеціальності) 172 «Телекомунікації та радіотехніка» Лазурко В.Є.

Прийняв: ас. каф. 501

Перетятько М. С.

Національна шкала:

Кількість балів:

Оцінка: ECTS

Харків 2021

Ціль роботи: Навчитися роботі у Terraform та створення облікового запису у GCP.

ХІД РОБОТИ

1)Створили обліковий запис у GCP
![image](https://user-images.githubusercontent.com/79759252/117302703-98f45e80-ae84-11eb-8102-cb725018c43c.png)
Рисунок 1 – Обліковий запис у GCP

\2) Встановив Terraform за допомогою команди choco install terraform

![image](https://user-images.githubusercontent.com/79759252/117302937-d6f18280-ae84-11eb-8b0c-38692f789b61.png)
Рисунок 2 – Установлення Terraform

\3) Створюємо каталог для прикладів в цьому керівництві і всередині нього збережіть наведений нижче приклад конфігурації в файл з ім'ям main.tf

terraform {

required_providers {

google = {

source = "hashicorp/google"

version = "3.5.0"

}

}

}

provider "google" {

credentials = file(".json")

project = "<PROJECT_ID>"

region = "us-central1"

zone = "us-central1-c"

}

resource "google_compute_network" "vpc_network" {

name = "terraform-network"

}

\4) Ініціалізіруємо нову конфігурацію Terraform, запустивши terraform init команду в тому ж каталозі, що і ваш main.tf файл.
![image](https://user-images.githubusercontent.com/79759252/117303486-68f98b00-ae85-11eb-9752-e8850f863658.png)
Рисунок 3 – Ініціалізація конфігурації Terraform

\5) Cтворення ресурсів за допомогою команди terraform apply
![image](https://user-images.githubusercontent.com/79759252/117304062-03f26500-ae86-11eb-97e6-0a3bbbc407a2.png)
![image](https://user-images.githubusercontent.com/79759252/117304089-08b71900-ae86-11eb-9d51-0b0522b9753c.png)

Рисунок 4 – Створення ресурсів

\6) Додавання ресурсів

У файл main.tf додаємо данні команди

resource "google_compute_instance" "vm_instance" {

name = "terraform-instance"

machine_type = "f1-micro"

boot_disk {

initialize_params {

image = "debian-cloud/debian-9"

}

}

network_interface {

network = google_compute_network.vpc_network.name

access_config {

}

}

}

terraform apply і yes

\7) Для зміни ресурсів ми вписуємо данну команду

+ tags = ["web", "dev"]

\8) Ресурси можуть бути знищені за допомогою terraform destroy

ВИСНОВКИ

В данній лабораторній роботі було виконано маніпуляції з GCP, а саме ми навчилися створювати обліковий запис на GCP. Навчився працювати з terraform. Також встановили за допомогою CHOCOLATEY terraform. Навчилися додавати, редагувати, та знищувати ресурси.
