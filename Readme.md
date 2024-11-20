# Analisis Teks : Klasifikasi Sentimen

**Halo Sobi**. Ini adalah projek pertama di akun ini, baca dan kasih masukan ya, slepet slebew.

**Quick Preview :**
  Jadi projek ini terkait analisis teks berupa klasifikasi sentimen menggunakan Machine Learning dan Deep Learning. Sebenernya ini dataset sederhana si, but that's not the point of this projek. Projek ini menggunakan beberapa algoritma Machine Learning dan Deep Learning dalam pemodelan sentimennya. Tapi dataset yang digunakan disini udah clean, jadi untuk _preprocessing_ nya agak ngawur karena main cepet aja wkwkkw.

**Apa si metode yang digunakan?**
Penelitian ini menggunakan beberapa metode di Machine Learning dan Deep Learning meliputi 
1. Support Vector Machine
2. Ridge Classifier
3. Rocchio Algorithm
4. Multinomial Naive Bayes
5. K-Nearest Neighbor
6. Logistic Regression
7. Light Gradient Boosting Machine
8. Dense Neural Network
9. Long Short-Term Memory (LSTM)
10. Bidirectional Long Short Term Memory (Bi-LSTM)
11. Gated Recurrent Unit
12. Indonesian Bidirectional Encoder Representation Transformer (IndoBERT)

Tapi ada banyak kekurangan di kodenya si sob, untuk algoritma Deep Learning yang digunakan 8 - 12 evaluasi tidak menggunakan Cross Validation, sehingga model yang dihasilkan belum cukup robust (handal). Cross Validation dilakukan untuk menguji model pada beberapa subset data sehingga dapat diuji kehandalannya pada berbagai bagian dataset [1].
![Alt text](https://lh4.googleusercontent.com/6u1bJFt9SNwVd91igYbODQR8O9p2mD5-9uJkeZTx_zFCDh0558iYSdexm-GX-eTUC2r7kpx1h7u3fzlPWuf2AeKb-EYmHYSyZbzcVxuuwTYd3dQ3FtkjmgQcUZpU_8lhyfrTeqkMpIHWJxiRduW5oZs)
***Sumber : https://dqlab.id/tipe-machine-learning-dengan-k-fold-cross-validation***

**Apa insight baru yang diperoleh dari projek tersebut?**
Jadi setelah melakukan pemodelan itu diperoleh hal-hal berikut sob.
- Metode terbaik adalah Logistic Regression. Berdasarkan pemodelan yang dilakukan metode berbasis linier menunjukkan performa terbaik. Sebenernya bukan linier juga si karena fungsi yang digunakan di RegLog itu sigmoid, cuma metode tersebut tergolong metode sederhana, namun mengungguli algoritma Deep Learning ataupun algoritma berbasis tree seperti Light GBM. Penulis menduga kayanya itu gara-gara data yang digunakan hanya mempertimbangkan 1 fitur, dimana metode berbasis tree ataupun deep learning cenderung unggul pada dataset berdimensi tinggi ataupun fitur kompleks [2][3].
- Data augmentasi menggunakan _back translation_ memberikan peningkatan yang cukup signifikan pada pemodelan yang dilakukan. Pada penelitian itu, kami menggunakan 2 bahasa target dalam proses _back translation_. Akurasi untuk _class_ minoritas yang awalnya 0 - 0.05 naik menjadi 0.21. Tentunya walaupun belum memiliki akurasi yang baik, namun peningkatan tersebut menunjukkan bahwa metode yang dilakukan berpengaruh terhadap hasil yang diinginkan.
- Pemodelan pada kasus klasifikasi selalu sertakan parameter **stratify = variabel target** saat splitting dengan fungsi train_test_split(). Hal itu bertujuan agar sampling pada proses splitting mempertimbangkan proporsi _class_ pada data latih ataupun data uji. Misal, jika class minoritas berjumlah 60 observasi, maka instead of sampling random sehingga ada kemungkinan 60nya masuk train (pengujian tidak dilakukan untuk class ini karena semuanya dimasukin ke data latih) atau 60nya masuk test (pelatihan tidak dilakukan untuk class ini karena semuanya dimasukin ke data uji), sampling stratifikasi menggunakan 48 observasi untuk train dan 12 observasi untuk test (jika proporsi train test 80:20) akan memberikan model yang lebih tepat. [4]
- Untuk memprediksi suatu input saat kamu mempunyai model yang sudah dilatih, inputnya harus diproses agar sesuai dengan input yang digunakan dalam pemodelan. Misal pada kode di atas menggunakan vectorizer TF-IDF.
- Teknik augmentasi seharusnya diterapkan ke data train saja. Kenapa?? Hal ini karena augmentasi itu seperti perluasan data tanpa mengumpulkan data baru. Misal menghasilkan data baru untuk data gambar dengan cara melakukan transformasi geometri pada suatu gambar, misal dirotasi, ataupun dizoom. Hal tersebut akan menghasilkan data baru dengan karakteristik berbeda namun secara umum masih memiliki kemiripan dengan data awalnya. Nah kondisi ini yang tidak boleh dilakukan pada pemodelan machine learning karena kebocoran informasi data testing pada data training _(data leakage)_. Kondisi itu terjadi ketika pelatihan tidak sengaja menggunakan data uji sehingga saat diuji tentunya model dapat mengenali data tersebut [5]. **Hal ini yang mendasari proses splitting perlu dilakukan terlebih dahulu sebelum proses pemodelan dimulai**.
  
## *Reference :*
1. Xiong, Z., Cui, Y., Liu, Z., Zhao, Y., Hu, M., & Hu, J. (2020). Evaluating explorative prediction power of machine learning algorithms for materials discovery using k-fold forward cross-validation. Computational Materials Science, 171, 109203.
2. Charbuty, B., & Abdulazeez, A. (2021). Classification based on decision tree algorithm for machine learning. Journal of applied science and technology trends, 2(01), 20-28.
3. Salehi, A. W., Khan, S., Gupta, G., Alabduallah, B. I., Almjally, A., Alsolai, H., ... & Mellit, A. (2023). A study of CNN and transfer learning in medical imaging: Advantages, challenges, future scope. Sustainability, 15(7), 5930.
4. https://scikit-learn.org/dev/modules/generated/sklearn.model_selection.train_test_split.html
5. Bernett, J., Blumenthal, D. B., Grimm, D. G., Haselbeck, F., Joeres, R., Kalinina, O. V., & List, M. (2024). Guiding questions to avoid data leakage in biological machine learning applications. Nature Methods, 21(8), 1444-1453.
