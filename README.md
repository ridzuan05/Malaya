# Malaya
NLTK like for bahasa Malaysia

## Requirements
  * Python >= 3.0
  * Tensorflow >= 1.3
  * NumPy >= 1.0
  * Sklearn >= 0.18
  * Fuzzywuzzy
  * unidecode
  * nltk
  * scipy

## Installation

1. Install dependencies
```bash
pip3 install sklearn fuzzywuzzy nltk unidecode numpy scipy python-levenshtein tensorflow==1.3
```

```python
import nltk
nltk.download('punkt')
```

2. Clone this repository
```bash
git clone https://github.com/DevconX/Malaya
```

3. install using setup.py
```bash
python3 setup.py install
```

## To do

- [x] tokenizer
- [x] stemming
- [x] tatabahasa gathering
- [x] Multinomial naive bayes
- [x] Naive Part-Of-Speech
- [x] number to words (currency, numbers, position, year)
- [ ] stopwords
- [x] normalizer
- [ ] corpus gathering
- [x] top-k hot topic (LSA, NMF, LDA)
- [ ] sentiment analysis
- [x] semantic and similar words searching
- [ ] bahasa malaysia checker

## Example

#### Check more in example/example.ipynb

```python
import malaya

print(malaya.stemming('makanan'))
-> makan

print(malaya.naive_POS_string('bapa sedang menulis surat'))
-> [('KN', 'bapa'), ('KETERANGAN', 'sedang'), ('KJ', 'menulis'), ('KN', 'surat')]

print(malaya.naive_POS_string('Dalam ayat pertama Kucing ialah pembuat, menangkap ialah perbuatan melampau dan seekor burung ialah benda yang kena buat atau penyambut'))
-> [('KS', 'dalam'),
 ('KN', 'ayat'),
 ('KJ', 'pertama'),
 ('KN', 'kucing'),
 ('KPEMERI', 'ialah'),
 ('KJ', 'pembuat'),
 ('', ','),
 ('KJ', 'menangkap'),
 ('KPEMERI', 'ialah'),
 ('KJ', 'perbuatan'),
 ('KJ', 'melampau'),
 ('KH', 'dan'),
 ('KJ', 'seekor'),
 ('KN', 'burung'),
 ('KPEMERI', 'ialah'),
 ('KJ', 'benda'),
 ('KETERANGAN', 'yang'),
 ('KN', 'kena'),
 ('KN', 'buat'),
 ('KH', 'atau'),
 ('KJ', 'penyambut')]

malaya.to_cardinal(123456789)
-> 'seratus dua puluh tiga juta empat ratus lima puluh enam ribu tujuh ratus lapan puluh sembilan'

malaya.to_ordinal(11)
-> 'kesebelas'

malaya.classify_bayes('kelulusan perlu melalui jawatankuasa')
-> negative: 0.589947
positive: 0.410053

corpus_normalize = ['maka','serious','yeke','masing-masing']
malaya.train_normalize(corpus_normalize)
malaya.user_normalize('masing2')
-> 'masing-masing'
malaya.user_normalize('srious')
-> 'serious'
```

#### Semantic search example, semantic-example/example-semantic-search.ipynb
```python
malaya.train_vector(corpus,10)
epoch: 1000, loss: 4.156271
epoch: 2000, loss: 3.501364
epoch: 3000, loss: 2.607565
epoch: 4000, loss: 2.888038
epoch: 5000, loss: 2.324599
epoch: 6000, loss: 2.288272
epoch: 7000, loss: 1.827932
epoch: 8000, loss: 2.251363
epoch: 9000, loss: 1.611805
epoch: 10000, loss: 1.972360
done train

malaya.semantic_search('mahathir')
-> [(0, 'mahathir'),
 (1, 'ketokohan'),
 (2, 'berfikiran'),
 (3, 'guru'),
 (4, 'tnb'),
 (5, 'menyebut'),
 (6, 'muda'),
 (7, 'bermasalah'),
 (8, 'mengharapkan'),
 (9, 'hasil')]

malaya.semantic_search('najib')
-> [(0, 'najib'),
 (1, 'dijadikan'),
 (2, 'mengatasi'),
 (3, 'tersedia'),
 (4, 'sampai'),
 (5, 'mencari'),
 (6, 'pucuk'),
 (7, 'restoran'),
 (8, 'stres'),
 (9, 'terhasil')]
```

#### k-topic modelling example, topic-example/example-topic.ipynb
```python
malaya.train_lda(corpus,10)
malaya.topic_lda(10)
-> [(0,
  'kemahirannya memainkan kawasan peranan membangun luar membangunkan antara berkongsi pengalaman'),
 (1,
  'penting berkembang negara harus mengeluarkan perlembagaan raya tersebut juga pilihan'),
 (2,
  'ros pemilihan parti perlembagaan umno melebihi tempoh bulan keputusan benar'),
 (3, 'nak bayar macam mana mdb tutup selepas sewa tanah rumah'),
 (4, 'kalau minta mca kita tidak daripada lah ada apaapa tahunan'),
 (5, 'dan kami dalam tidak yang dengan untuk ia ini itu'),
 (6, 'yang dan dalam dengan menteri oleh itu seperti pengalaman telah'),
 (7, 'dan yang kita di akan dalam ini untuk saya itu'),
 (8, 'sebab akan tumpuan pada di dan untuk mahu rm harga'),
 (9, 'ada global perlu kerana kita pas pengalaman baiah percaya pilihanraya')]

malaya.train_nmf(corpus,10)
malaya.topic_nmf(10)
-> [(0, 'yang dan dalam malaysia di dengan negara telah kepada itu'),
 (1, 'kita akan kalau bahasa ppsmi tak nak inggeris ilmu ambil'),
 (2, 'saya mungkin itu harap perlu membuat diri cina adalah tetapi'),
 (3, 'kami akan dan itu tiada dalam jppm pihak pesawat keduadua'),
 (4, 'ini masa untuk pada adalah rakyat bukan terus meningkatkan dan'),
 (5, 'tidak ada lagi pernah kerajaan pas boleh berlaku politik bulan'),
 (6, 'kapal jho low tak di itu ada dirampas dah mana'),
 (7, 'berjalan lancar gembira projek ia amat melihat dengan semakin saya'),
 (8,
  'parti ros umno pemilihan perlembagaan keputusan kebenaran melebihi bersatu dah'),
 (9, 'orang asli masyarakat jakoa menjadi temiar harus mereka kerana sumber')]

malaya.train_lsa(corpus,10)
malaya.topic_lsa(10)
-> [(0, 'dan yang kita dalam akan ini itu kami untuk dengan'),
 (1, 'kita kalau ini tak masa rakyat bahasa ada nak parti'),
 (2, 'saya tidak ada itu yang menteri mungkin mdb perdana tak'),
 (3, 'kami tidak akan itu ada parti tak mereka kita tiada'),
 (4, 'dalam negara ada tidak dengan yang pengalaman pas berkongsi mempunyai'),
 (5, 'tidak ia dengan ada lagi kerajaan pas berjalan pernah boleh'),
 (6, 'ini mereka masa pada parti yang kepada bukan oleh ros'),
 (7, 'dengan ia berjalan parti umno lancar ros pemilihan saya dan'),
 (8, 'untuk orang asli di ada ia kerajaan kapal malaysia bulan'),
 (9, 'yang di menteri untuk keputusan perdana ada sebelum apa sudah')]
```

## Warning

Install this library with fully aware that this library is still in alpha stage.

There is no type checking, no assert. Still on development process.

Part Of Speech will not yet binded with any corpuses, I still having a problem with Dewan Pustaka.

Also, I cannot released primary corpuses for sentiment analysis and normalizer YET because got corporate issues.

Documentation will be released soon.

## Disclaimer

Most of the data gathered using crawlers crawled through targeted malaysia websites. I am not aware of any data protection.

## Authors

* **Husein Zolkepli** - *Initial work* - [huseinzol05](https://github.com/huseinzol05)
