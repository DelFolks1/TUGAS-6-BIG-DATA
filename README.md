<h1> Tugas 6 Big Data </h1> 
Nama : Raja Permata Boy <br>
NRP : 05111740000070 <br>
<h1> Spark Compiled Model Using KNIME </h1>
<h2>MLlib model to PMML</h2>
<h3>Business Understanding</h3>
Proses yang dapat dilakukan pada dataset :<br>
- Menentukan klasifikasi dari spesies bunga<br>
- Digunakan dalam data mining dan machine learning<br>
<h3>Data Understanding</h3>
<img src="/docbd6/dataset1.jpg">
Dilihat dari kolom dan data-data yang digunakan pada dataset ini, kita bisa melihat bahwa dataset yang digunakan adalah Iris Flower Dataset. <br>
Data set ini memiliki 3 kelas dan memiliki  5 kolom :<br>
- sepal_length <br>
- sepal_width<br>
- petal_length<br>
- petal_width<br>
- species<br>
<h3>Data Preparation</h3>
<img src="/docbd6/dataprep.jpg">
Buat spark context local dengan Create Local Big Data Environment<br>
Lalu, dataset dibaca dengan menggunakan File Reader <br>
Untuk memasukkan tabel KNIME ke dataframe digunakan Table to Spark<br>
Berikut konfigurasi untuk tiap node : <br>
Konfigurasi Create Local Big Data Environment <br>
<img src="/docbd6/createbd.jpg"><br>
Konfigurasi node File reader <br>
<img src="/docbd6/filereader.jpg"><br>
Konfigurasi Table To Spark <br>
<img src="/docbd6/tabletospark.jpg"><br>
<h3>Modelling</h3><br>
<img src="/docbd6/modelling.jpg"><br>
Model ditrain di Spark dengan menggunakan Spark k-Means<br>
Lalu, model diubah ke PMML dengan menggunakan node Spark MLlib to PPML<br>
Terakhir, PMML diubah ke java dengan menggunakan node PMML compiler<br>
Berikut konfigurasi dari tiap node :<br>
Spark k-Means :<br>
<img src="/docbd6/kmeans.jpg"><br>
MLlib To PMML<br>
<img src="/docbd6/mllibtopmml.jpg"><br>
PMML Compiler :<br><br>
<img src="/docbd6/pmmlcomp.jpg"><br>
<h3>Evaluation </h3>
<img src="/docbd6/evaluation.jpg"><br>
Pertama, dataset dibaca dengan menggunakan node File Reader <br>
Selanjutnya, kita menggunakan node Compiled Model Predictor untuk membuat prediction<br>
Terakhir, kita menggunakan node Entropy Scorer untuk menghitung entropi dari prediction yang ada<br>
Hasil dari Entropy Scorer :
<img src="/docbd6/entropy.jpg"><br>
<h3>Deployment </h3>
<img src="/docbd6/deployment.jpg"><br>
Kita menggunakan Container Input (JSON) untuk memasukkan dataset iris<br>
Lalu, kita menggunakan node JSON To Table untuk mengubah JSON kedalam bentuk table multi kolom <br>
Setelah itu, kita menambahkan node Compiled Model Predictor untuk membuat prediction. <br>
Tambahkan lagi node Table to JSON untuk mengubah table ke dalam bentuk table<br>
Terakhir, tambahkan node Container Output (JSON)  untuk memperlihatkan cluster dari Iris dataset dalam JSON output<br> 
Hasil Output JSON :
<img src="/docbd6/outputjson.jpg"><br>
<br>
<h2>Spark Compiled Model Predictor</h2>

<h3>Business Understanding</h3>
Proses yang dapat dilakukan pada dataset :<br>
- Menentukan klasifikasi dari spesies bunga<br>
- Digunakan dalam data mining dan machine learning<br>
<h3>Data Understanding</h3>
<img src="/docbd6/dataset1.jpg">
Dilihat dari kolom dan data-data yang digunakan pada dataset ini, kita bisa melihat bahwa dataset yang digunakan adalah Iris Flower Dataset. <br>
Data set ini memiliki 3 kelas dan memiliki  5 kolom :<br>
- sepal_length <br>
- sepal_width<br>
- petal_length<br>
- petal_width<br>
- species<br>
<h3>Data Preparation</h3>
<img src="/docbd6/dataprep2.jpg">
Pertama, baca data dengan menggunakan Filer reader <br>
Lalu, tambahkan node Decision Tree Learner untuk membuat decision tree<br>
Lalu, tambahkan noded RPop MLP Learner untuk membuat trained neutral network <br>
Keduanya lalu disambungkan ke node PMML To Cell untuk mengubah PMML port menjadi cell PMML <br>
 
<h3>Modelling</h3><br>
<img src="/docbd6/modelling2.jpg"><br>
Kedua node PMML To Cell tadi kita gabungkan dengan menggunakan Concatenate<br>
Lalu, kita tambahkan node Table To PMML Ensemble untuk menggabungkan table PMML menjadi satu dokumen PMML dengan model mining <br>
Kemudian menambahkan node PMML Compiler untuk menerjemahkan model PMML ke Java yang nantinya akan dijalankan oleh node Spark Compiled Model Predictor <br>
