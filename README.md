# Практично-лабораторне заняття №9

Тема: Неперервна доставка.

Мета: ознайомитися з принципами і практиками неперервної доставки, сформувати навички роботи з хмарними сервісами Azure.

## 1. Зайдемо в Azure Portal та створимо ресурсну групу з назвою lookup-rg.
   
![image](https://github.com/user-attachments/assets/d3745e39-3f13-4b71-a3f1-73dd18c309da)

![image](https://github.com/user-attachments/assets/807a9e52-5ca2-4885-b4bf-b283baccb0a3)

Створимо всередині ресурсної групи App Servicе.

![image](https://github.com/user-attachments/assets/f33c6281-5ec4-48ce-bbdb-a1abf0d36f66)


## 2. Створимо service principal через Bash у порталі Azure.

![image](https://github.com/user-attachments/assets/6ab9d4ef-76ed-4a30-89c2-dad9132856c4)

## 3. Додамо секрет у GitHub.

Скопіюємо вивід та в GitHub репозиторію відкриємо Settings - Secrets and variables - Actions - New repository secret.

![image](https://github.com/user-attachments/assets/7b90f78a-9b10-4cf3-9838-29737f6b84e2)

![image](https://github.com/user-attachments/assets/29efcbf8-2106-45d3-9988-cffbaa01c475)

Вставимо скопійований код. Результат:

![image](https://github.com/user-attachments/assets/0020d84a-aa03-43af-8050-17e36472d86d)

## 4. Додамо job до GitHub Actions.

![image](https://github.com/user-attachments/assets/11fbc684-8a3b-4649-8050-cd14c7a40643)

Перевіримо:

![image](https://github.com/user-attachments/assets/e067cc08-1cf2-41ed-adcc-30b5bc2bb14b)

Перейдемо за посиланням:

![image](https://github.com/user-attachments/assets/eb0a126f-bf14-44f6-856f-6e8cf92236d4)

![image](https://github.com/user-attachments/assets/303d398f-af11-4240-afba-98cad439a7ff)

**Коментарі до коду в GitHub:**

```deploy:``` - назва другого завдання (job) у workflow.

```runs-on: ubuntu-latest``` - job буде виконуватись на віртуальній машині з Ubuntu останньої версії.

```needs: build``` - deploy почнеться тільки після успішного завершення build.

```steps:``` - початок списку кроків для виконання цього завдання.

Авторизація у Microsoft Azure:

```
- name: Log in to Azure
      uses: azure/login@v2
      with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}
```

Розгортання:

```
- name: Deploy to Azure Web App
      uses: azure/webapps-deploy@v2
      with:
        app-name: lookup-frontend //назва веб-застосунку в Azure, куди потрібно розгорнути проєкт
        images: ghcr.io/mikunajanari/bryzhyniuk_lb8:latest //Docker-образ, який потрібно задеплоїти
```
