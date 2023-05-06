# Виконання роботи

Встановимо terraform через Power Shell за допомогою команди:

```
choco install terraform
```

Після інсталяції ми переходимо до GCP і створюємо новий проект

![](A1.png)

Після створення проекту і активації Compute Engine API переходимо в наш проект і натискаємо IAM and Admin. Після того як ми перейшли по цій вкладці встановлюємо та налаштовуємо Service Accounts.

![](A2.png)

Натискаємо + CREATE SERVICE ACCOUNT

![](A3.png)

Тиснемо на вкладку create service account  і переходимо в налаштування де задаються назва, ID та ролі та створюємо service account. 

![](A4.png)

Перейдемо у вкладку Manage keys та створимо ключ, після чого зберігаємо у себе на ПК: А також активуємо наш ключ.

![](A5.png)

Вибираємо формат JSON

![Изображение выглядит как текст, снимок экрана, Шрифт, программное обеспечение

Автоматически созданное описание](Aspose.Words.3f932b91-db40-4495-9dbd-74bcae2701e8.006.png)

Активований ключ

![](A7.png)

![](A8.png)

Починаємо налаштування Terraform

Тепер після створення аккаунта нам потрібно створити для Terraform папку в якій будуть зберігається дані туди ж ми і перенесемо наш ключ і створимо файл main.tf

Створюємо три файли типу (main, variables, outputs).tf в яких буде записан певний код. У main вказується Terraform, що працюватиме із GCP, створюється network та subnetwork, 

![](A9.png)

у vm\_instance задаємо 5 тегів з будь яким ім’ям(без великих літер на пробілів, бо буде викликати похибку), та конфігуруємо firewall(брандмауэр). В variables вказуємо Project ID:назву та назву файлу з ключем.

Відкриваємо створений нами файл і запишемо наступний код

main.tf:
```
terraform {

`	`required\\_providers {

`	 `google = {

`	 `source = "hashicorp/google"

`	 `version = "4.51.0"

`		`}

`	`}

}
```

Тут ми вказуємо terraform, що він повинен працювати в GCP і вказуємо версію.
```
provider "google" {

credentials = file(var.credentials\_file)

project = var.project

region = var.region

zone = var.zone

}
```

Тут ми вказуємо дані необхідні для роботи, ключ, наш проект, регіон та зону. 


```
resource "google\_compute\_network" "vpc\_network" {

name = "servist"

}

resource "google\_compute\_subnetwork" "LABA3\_subnetwork"{

name = "var.machine\\_name"

network = google\_compute\_network.vpc\_network.name

ip\_cidr\_range = "10.0.0.0/16"

region = var.sub-region

}
```

Ім'я обрано, регіон буде зазначено у файлі "variables.tf". 

Перейдемо до створення віртуальної машини. По-перше задамо ім'я labprod3 та конфігурацію машини e2-micro.
```
resource "google\_compute\_instance" "vm\_instance" {

name = "labprodject3"

machine\_type = "e2-micro"

tags = ["lemon", "orange", "apple", "lime", "kiwi"]

boot\_disk {

initialize\_params {

image = "debian-cloud/debian-11"

}

}

network\_interface {

network = google\_compute\_network.vpc\_network.name

subnetwork = google\_compute\_subnetwork.LR3\_subnetwork.name

access\_config {

          }

     }

   }
```
Перейдемо до файлу "variables.tf"

Запишемо наші дані в цей файл
```
variable "projectlr3" {

default = "laba3-l3"

}

variable "credentials\_file" {

default = "<a name="_hlk134258507"></a>laba3-l3.json"

}

variable "region" {

default = "us-central1"

}

variable "zone" {

default = "us-central1-c"

}

variable "machine\\_name" {

default = " laba3-l3-1"

}
```

Тепер запишемо в файл outputs.tf наступну команду
```
output "ip\\_intra" {

`	`value = google\\_compute\\_instance.vm\\_instance.network\\_interface.0.network\\_ip

}

output "ip\\_extra" {

`	`value = google\\_compute\\_instance.vm\\_instance.network\\_interface.0.access\\_config.0.nat\\_ip

} 
  }
```
Цей код відасть нам IP-адресою машини при виконані terraform apply.

Перейдемо до cтворення ВМ

Зайшовши в термінал від іменни адміністратора пишемо команду cd і назва нашої папки в якій лежать наші файли, а після пишемо команду

terraform init

і натискаємо Enter

![](A10.png)

далі пишемо

terraform apply

Ми бачимо план, що зробить terraform і нам потрібно підтвердити його дії Після натискання YES, почнеться створення віртуальної машини

![](A11.png)

Після успішного створення віртуальної машини, повернемося в GCP і перевіримо наявність нашої машини

![](A12.png)

Як можна побачити ВМ ми створили правильно

![](A13.png)

Тепер видалимо ВМ за допомогою команди

terraform destroy

Після введення цієї команди на питання чи згодні ми на видалення пишемо YES

![](A14.png)

Тобто, якщо подивимось уважно, terraform все видалив,  відпрацював коректно![Изображение выглядит как текст, снимок экрана, Шрифт, программное обеспечение

Автоматически созданное описание](Aspose.Words.3f932b91-db40-4495-9dbd-74bcae2701e8.015.png)

# Висновок:

У  цій лабораторній ми використовували terraform і за допомогою його створили віртуальну машину у GCP, а також мережі. Створювали SERVICE ACCOUNT і налаштовувати його. terraform ми можемо використовувати  для створення хмарної інфраструктури в cloud і управляти нею за допомогою .TF файлів. Це дозволяє нам автоматизувати процес створення віртуальної машини або створення мереж.

