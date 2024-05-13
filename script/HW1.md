##1) Скачала 3 рана по ссылкам и поместила их в папку dataset:

https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR16080651&display=download
https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR16080652&display=download
https://trace.ncbi.nlm.nih.gov/Traces/?view=run_browser&acc=SRR16080653&display=download
 
создала файл manifest.txt в которм содержатся данные(синтаксис сохранен):

sample-id,absolute-filepath,direction<br /> 
SRR16080651,/home/card/microbioms/HW1/dataset/SRR16080651.fastq,forward
SRR16080652,/home/card/microbioms/HW1/dataset/SRR16080652.fastq,forward
SRR16080653,/home/card/microbioms/HW1/dataset/SRR16080653.fastq,forward

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
