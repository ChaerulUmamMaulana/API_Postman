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

9. Lalu Klik Script, jgn lupa pilih Post-response dan masukan code: // Postman → Tests tab: 
if (pm.response.code === 200) { 
const json = pm.response.json(); 
console.log("Email verifikasi dikirim ke:", json.email); 
console.log("Sekarang buka inbox email dan klik link verifikasi."); 
console.log("Setelah klik, lanjut ke Step 3 untuk cek status."); 
} else { 
console.log("Gagal kirim email:", pm.response.json().error.message); 
}  
<img width="1334" height="845" alt="image" src="https://github.com/user-attachments/assets/97842d50-20cb-490a-8316-827aee597e7e" />

10. Setelah melakukan semua Set-Up Klik send dan Cek Email yang di daftarkan
    <img width="1328" height="1011" alt="image" src="https://github.com/user-attachments/assets/6b171b56-8a46-4713-9ac9-d82d6af1fa55" />

11. Buka Email yang didaftarkan dan pastikan ada Link seperti berikut
    <img width="1919" height="893" alt="image" src="https://github.com/user-attachments/assets/726972a5-bf97-4702-8e15-476e487ab925" />

12. Klik Link Tersebut dan Berhasil Verifikasi
    <img width="1778" height="517" alt="image" src="https://github.com/user-attachments/assets/c557d7ff-40b2-402d-9b6d-990fba70edf9" />

    Langkah selanjutnya adalah Cek Verifikasi Email dan bisa melalui 2 cara, yaitu: langsung dari Firebase dan Via BackEnd

    Cara A :
    1. Bisa langsung dilakukan langsung dengan URL : https://identitytoolkit.googleapis.com/v1/accounts:lookup?key={
{FIREBASE_API_KEY}} , Pastikan Methodnya POST, dan salin link tersebut
    2. Pada Body masukan code seperti yang tertera
       <img width="1367" height="755" alt="image" src="https://github.com/user-attachments/assets/91b48f87-8d2b-41db-bbce-f0b329ce49ef" />
    3. Dan Send Hasilnya akan seperti ini
       <img width="1335" height="1003" alt="image" src="https://github.com/user-attachments/assets/4cdc02cf-58a0-4b28-9144-8c1489776a50" />


    Cara B :
    1. Salin URL berikut: {{BACKEND_BASE_URL}}/auth/verify-token
    2. Masukan code seperti yang tertera
    3. pada header masukan key: Content-Type dan Accept, Valuenya keduanya sama yaitu: Application/json
       <img width="1356" height="769" alt="image" src="https://github.com/user-attachments/assets/9bb9f9b1-2b7c-4eab-8bce-af812e5194dd" />

    Langkah selanjutnya yaitu login, dengan Login Email dan Password

    1. Masukan URL berikut: https://identitytoolkit.googleapis.com/v1/accounts:signInWithPa
ssword?key={{FIREBASE_API_KEY}}
    2. Untuk Body :{ 
    "email": "{{USER_EMAIL}}", 
    "password": "{{USER_PASSWORD}}", 
    "returnSecureToken": true 
} 
<img width="1360" height="872" alt="image" src="https://github.com/user-attachments/assets/da0e6e47-2c91-45d6-b927-c07613380197" />


   3. untuk Script nya : // Postman → Tests tab: 
const json = pm.response.json(); 
Tunggu beberapa menit 
if (pm.response.code === 200) { 
// Update environment dengan idToken BARU hasil login 
pm.environment.set("FIREBASE_ID_TOKEN", json.idToken); 
pm.environment.set("FIREBASE_REFRESH_TOKEN", json.refreshToken); 
console.log("Login berhasil. Token diperbarui."); 
console.log("Lanjut ke Step 5: kirim token ke backend."); 
} else { 
console.log("Login gagal:", json.error.message); 
} 
<img width="1369" height="829" alt="image" src="https://github.com/user-attachments/assets/8644f386-d940-4f4a-bf7e-ce584df04e29" />

  4. Klik Send, maka hasil seperti ini
     <img width="1354" height="978" alt="image" src="https://github.com/user-attachments/assets/4793e03a-33f5-46f7-a2df-1f9845b4c965" />

pada tahap ini kita memang tidak bisa mengedit secara full keseluruhan Body nya, tapi disini kita bisa mengubah Sender Name dan From, seperti gambar berikut:
<img width="1521" height="890" alt="image" src="https://github.com/user-attachments/assets/092ef408-13fb-42e1-bd80-2ddb13d7074f" />




       
       





   



   
   









