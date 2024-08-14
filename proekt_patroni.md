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

### 2. 
