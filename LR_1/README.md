**Виконання роботи**

1. Створили обліковий запис GitHub

![](Aspose.Words.aa467fc5-1351-4a3a-a548-106e7981e185.001.png)

2. Встановили CHOCOLATEY за допомогою powershell:

Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))

3. Встановили git на комп'ютер за допомогою Chocolatey:

choco install git -y

Перевірили правильність установки. Для цього дізнаємось версію встановленого git.

![Изображение выглядит как текст

Автоматически созданное описание](Aspose.Words.aa467fc5-1351-4a3a-a548-106e7981e185.002.png)

4. Налаштували гіт за своїми даними:

<a name="_hlk134143366"></a>git config --global user.name "MarynaTraichenkova"

git config --global user.email <a name="_hlk134152387"></a>traychenkova@gmail.com

5. Згенерували новий SSH ключ:

ssh-keygen -t ed25519 -C "traychenkova@gmail.com"

![Изображение выглядит как текст, Шрифт, линия, снимок экрана

Автоматически созданное описание](Aspose.Words.aa467fc5-1351-4a3a-a548-106e7981e185.003.png)

6\.  Створили новий репозиторій з назвою такою ж як і назва акаунту:

![Изображение выглядит как текст, снимок экрана, Шрифт, программное обеспечение

Автоматически созданное описание](Aspose.Words.aa467fc5-1351-4a3a-a548-106e7981e185.004.png)

5. Склонувати репозиторій за допомогою git clone на локальний пк та відредагувати README.md:

![Изображение выглядит как текст, снимок экрана, программное обеспечение, Мультимедийное программное обеспечение

Автоматически созданное описание](Aspose.Words.aa467fc5-1351-4a3a-a548-106e7981e185.005.png)

9. Завантажили опис профілю:

git add .

git commit -m "Add your comment"

git push

10. Висновок

У данній лабораторної роботи було здобуто знання щодо використання git та GitHub. Спочатку реєструвалися на GitHub та створили власний акаунт. Розглянуто роботу з репозиторієм.  А в завершені створили невеличке резюме.

