# API_Postman
Menguji API tanpa coding Flutter dulu. Autentikasi berbasis firebase,melalui pendekatan step-by-step.

Berikut tahapan awal dalam memulai pengujian dari firebase console:

1. Masuk Firebase "https://firebase.google.com/"
<img width="1914" height="945" alt="Screenshot 2026-03-10 083613" src="https://github.com/user-attachments/assets/2e552d95-580c-476f-a82d-f522957b1085" />

2. Buat Project dengan Klik "Go To Console"
   <img width="1919" height="972" alt="image" src="https://github.com/user-attachments/assets/66434566-bf0c-4eda-bfa2-a409ecf22272" />

3. Buat Project baru "Create a new Firebase Project"
   <img width="1918" height="952" alt="image" src="https://github.com/user-attachments/assets/f20ff872-013e-4ed3-b9f5-877ef4182462" />

4. Setelah membuat project, aktifkan autentikasi pada email/password
   <img width="1910" height="946" alt="image" src="https://github.com/user-attachments/assets/c13d2b56-8a57-4c07-9ff7-e5c8fbd2c95a" />

5. Pergi ke Settings, Klik General, tambahkan add app
   <img width="1913" height="936" alt="image" src="https://github.com/user-attachments/assets/9d896553-9276-4818-a814-3e1e246ca301" />

6. Buat Web App
   <img width="1912" height="944" alt="image" src="https://github.com/user-attachments/assets/f441f808-8a57-441f-ab0c-8bd7f0887b32" />

7. Ketika sudah menambahkan Web App, Android App, pada bagian Web App salin API KEY nya
   <img width="1913" height="934" alt="image" src="https://github.com/user-attachments/assets/16abb845-97fc-415c-9e3b-57926785952d" />

   Kemuddian buka PostMan untuk membuat environment, setelah menyelesaikan setUp pada Firebase Console, seperti menambahkan Add App dan Menyim;pan API Key
Buka Aplikasi PostMan:

1. Buat Enviroment, disini saya menamakan Enviromentnya yaitu "Firebase Auth Dev"
   <img width="1905" height="1005" alt="image" src="https://github.com/user-attachments/assets/70c72076-3ac4-4899-8286-0e49f9f07bea" />

2. Berikan Varibel dan Valuenya
   <img width="1919" height="1009" alt="image" src="https://github.com/user-attachments/assets/fa6e31bd-c940-409a-a1a1-ff2b3cb245b5" />

3. Buat Method pertama yaitu Sign In, dengan menggunakan URL berikut: https://identitytoolkit.googleapis.com/v1/accounts:signUp?               key=AIzaSyBweyAv9wvBiSDSvfuO9RMwRTXnVn3cBOg, Ubah Method menjadi POST
   <img width="1918" height="818" alt="Screenshot 2026-03-10 190630" src="https://github.com/user-attachments/assets/45ccdcbf-de39-4ce8-b970-2c78a4d7eae7" />

4. Masuk ke Body dan dan ubah menjadi RAW, dan masukan code seperti yang tertera
   <img width="1329" height="559" alt="image" src="https://github.com/user-attachments/assets/c9f1d9d0-db0e-4df3-ab04-d32ea3ed18db" />

5. Masuk Header Masukan Key: Content-Type dan value: application/json
   <img width="1346" height="686" alt="image" src="https://github.com/user-attachments/assets/188d6997-ddd5-435a-90fa-8f0a8cda661e" />

6. Masukan code pada Script, pada bagian Post-Response untuk untuk AutoSave Id Token seperti berikut: ( // Postman → Tests tab:
const json = pm.response.json();
if (pm.response.code === 200) {
pm.environment.set("FIREBASE_ID_TOKEN", json.idToken);
pm.environment.set("FIREBASE_LOCAL_ID", json.localId);
pm.environment.set("FIREBASE_REFRESH_TOKEN", json.refreshToken);
console.log("Register sukses. UID:", json.localId);
console.log("PERHATIAN: Email belum diverifikasi. Lanjut ke Step 2.");
} else {
console.log("Register gagal:", json.error.message);
} )
   <img width="1344" height="690" alt="image" src="https://github.com/user-attachments/assets/08a29a15-f9f1-4859-bcc4-d1523d05b8f9" />

7. Lalu buat Method baru untuk coba verification email, dengan URL berikut:https://identitytoolkit.googleapis.com/v1/accounts:sendOobCode?key={{FIREBASE_API_KEY}}, dan ubah method menjadi POST
   <img width="1919" height="498" alt="image" src="https://github.com/user-attachments/assets/c6e5ff00-c655-4613-b468-ceeadee601e3" />

8. Pada bagian body masukan code seperti berikut: ( {
"requestType": "VERIFY_EMAIL",
"idToken": "{{FIREBASE_ID_TOKEN}}"
} )
   <img width="1350" height="639" alt="image" src="https://github.com/user-attachments/assets/4184f318-76a6-4e98-8ecb-722c3a604d95" />

9. 

   



   
   









