##1) Скачала 3 рана по ссылкам и поместила их в папку dataset:

https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR16080651&display=download
https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR16080652&display=download
https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR16080653&display=download
 
создала файл manifest.txt в которм содержатся данные(синтаксис сохранен):

sample-id,absolute-filepath,direction<br /> 
SRR16080651,/home/card/microbioms/HW1/dataset/SRR16080651.fastq,forward
SRR16080652,/home/card/microbioms/HW1/dataset/SRR16080652.fastq,forward
SRR16080653,/home/card/microbioms/HW1/dataset/SRR16080653.fastq,forward

создала окружение и установила qiime2


задала переменные: (не знаю зачем, не использовала потом)
``` bush
input_reads=/home/card/microbioms/HW1/dataset
manifest=/home/card/microbioms/HW1/manifest.txt
output_qza=/home/card/microbioms/HW1/qiime_formatted
classifier=/home/card/microbioms/HW1/silva138_AB_V4_classifier.qza
```
Запуск qiime2:
```
 qiime tools import   --type 'SampleData[SequencesWithQuality]'   --input-path manifest.txt   --output-path output.qza   --input-format SingleEndFastqManifestPhred33
```

Запуск deblur:
```
qiime deblur denoise-16S --i-demultiplexed-seqs output.qza --p-trim-length 150 --p-sample-stats --o-representative-sequences rep-seqs-deblur.qza --o-table table-deblur.qza --o-stats deblur-stats.qza
```
```
feature_table=/home/card/microbioms/HW1/table-deblur.qza
rep_seqs_qza=/home/card/microbioms/HW1/rep-seqs-deblur.qza
qiime tools export --input-path $rep_seqs_qza --output-path HW1/after_deblur
rep_seqs=denoise_out/after_deblur/dna-sequences.fasta
qiime tools export --input-path deblur-stats.qza --output-path denoise_out/
```
```
mkdir taxonomy
qiime feature-classifier classify-sklearn --i-classifier $classifier --i-reads $rep_seqs_qza --o-classification "taxonomy/taxonomy.qza" --p-confidence 0.94
```









