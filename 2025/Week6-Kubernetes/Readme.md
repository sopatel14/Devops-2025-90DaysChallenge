This is the project forked from https://github.com/Amitabh-DevOps/Springboot-BankApp
All my manifest files are stored in Week 6 k8s




1. Kubernetes Cluster Proof
 
   kubectl get nodes
<img width="402" height="77" alt="image" src="https://github.com/user-attachments/assets/c3f0aec7-3054-4b34-b53a-5df57e778780" />

3. Complete Application Stack
   
   kubectl get all -n bank-app
   <img width="599" height="226" alt="image" src="https://github.com/user-attachments/assets/2be106c8-ea01-4627-b427-c7376c5bf6ec" />
   <img width="829" height="254" alt="image" src="https://github.com/user-attachments/assets/30f47552-bac8-4a11-a90c-28521f901931" />
   <img width="857" height="147" alt="image" src="https://github.com/user-attachments/assets/bf3a7f94-0be7-46bc-966b-e3557a170c03" />

4. Auto-scaling Configuration
 
   kubectl get hpa -n bank-app
   kubectl describe hpa -n bank-app

   <img width="917" height="235" alt="image" src="https://github.com/user-attachments/assets/e5fb53c9-ef99-4ba2-9b2d-edbe5ef3a924" />

6. Persistent Storage
 
   kubectl get pv,pvc -n bank-app
   kubectl describe pvc -n bank-app
   <img width="945" height="203" alt="image" src="https://github.com/user-attachments/assets/e240ea15-5fd7-4294-9ae3-c50c5e9b9a6e" />
   <img width="533" height="290" alt="image" src="https://github.com/user-attachments/assets/7057f968-6616-4004-a9b9-1e16e7f46cfb" />

8. Security Implementation
 
    kubectl get roles,rolebindings,networkpolicies -n bank-app
    kubectl describe role admin-role -n bank-app
    <img width="540" height="171" alt="image" src="https://github.com/user-attachments/assets/72ec13ed-b4e5-4c5c-83b7-8ff2b8a9a525" />
    <img width="575" height="140" alt="image" src="https://github.com/user-attachments/assets/347df751-7e1a-44c6-8057-8469cf38cf59" />
    
10. Advanced Features

   kubectl get crd | grep bank
   kubectl get cronjobs,jobs -n bank-app
   kubectl get bankapplications -n bank-app
   <img width="581" height="186" alt="image" src="https://github.com/user-attachments/assets/9dc0bd81-3bc0-458d-ab65-124c0ebc079b" />





<img width="908" height="434" alt="image" src="https://github.com/user-attachments/assets/07ebda2e-1ddd-4f84-afac-2f20571aa9ce" />

   
   


