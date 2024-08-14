**Цель:**  

### Создание отказоуйстойчивого кластера на базе Patroni  

********************************

## Будем использовать 8 виртуальных машин  
3 ВМ - Postgresql + patroni  
3 ВМ - etcd   
2 BM - haproxy + keepalived  
*******************************  
### Кол-во задействанный ВМ  
![image](https://github.com/user-attachments/assets/ae8b8b2d-0bea-4e95-9069-eb3fb3fd2a7b)  

### Реализуем данную схему  
![image](https://github.com/user-attachments/assets/35935780-a0a8-454d-86b3-e159668610d7)  

### 1. Ставим кластер из 3-х нод etcd  

![image](https://github.com/user-attachments/assets/148d210e-99ee-4d7e-a932-446e6d0836bb)  

### 2. Patroni  
![image](https://github.com/user-attachments/assets/4cc743ae-2301-47ad-abb9-8eb4c7c092d1)  

### 3. Делаем switchover (ручное переключение)  
![image](https://github.com/user-attachments/assets/5b1308ab-ff24-4bc7-84c3-f6cd60863e1e)  

### 4. Смотрим черех haproxy на web-форме  
![image](https://github.com/user-attachments/assets/9e95103d-a4ed-4f08-92d1-aa87e7cbb557)  
и после смены результат   
![image](https://github.com/user-attachments/assets/ab654424-321c-434d-a934-a1422558deb3)  

Видим ,что лидер поменялся на vm3  

### 5. Также посмотрим на второй ноде haproxy  
было  
![image](https://github.com/user-attachments/assets/cbbb2790-8da9-48a1-8eab-459812b38ccb)  
стало  
![image](https://github.com/user-attachments/assets/9b1db0e0-5b17-4831-ad58-ab76785f33ff)  



### 6. Теперь пробуем автоматическое переключение (failover)  

![image](https://github.com/user-attachments/assets/05adb547-3d03-4375-9a8c-b807caf2a791)  

c vm3 перешло управление на vm2 у кого статус Sync Standby  
ну и смотрим в haproxy  
![image](https://github.com/user-attachments/assets/1234185d-1417-4a37-8afb-155116e517da)    
и на второй ноде (192..159)  
![image](https://github.com/user-attachments/assets/0a1f66a9-a8d8-4126-b03d-4fd37cf667c2)  

### 7. Теперь проверим подключение к нашей бд по виртуальному ip  
![image](https://github.com/user-attachments/assets/9f5ab1bc-fc58-40bb-8278-98b48effcb6e)  
подключение прошло успешно с обоих нодд haproxy по виртуальному ip  

### 8. Теперь остановим keepalived службу на haproxy2 и проверим что будет  
![image](https://github.com/user-attachments/assets/9352dd04-8a5b-41ae-b46e-ed9826ed2d1f)  
Мы видим ,что виртуальный ip перешел на haproxy 1-ю ноду.  
Подключение также присутствует  
Зашли в psql по виртуальному ip  




### 9.
